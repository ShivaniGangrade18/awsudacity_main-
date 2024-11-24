#!/usr/bin/env python3
# -*- coding: utf-8 -*-
# */AIPND-revision/intropyproject-classify-pet-images/check_images.py
#
# PROGRAMMER: Your Name
# DATE CREATED: 11/14/2024
# REVISED DATE: 
# PURPOSE: Classifies pet images using a pretrained CNN model, compares these
#          classifications to the true identity of the pets in the images, and
#          summarizes how well the CNN performed on the image classification task. 

from time import time
from print_functions_for_lab_checks import *  # Import custom functions to print and verify results
from get_input_args import get_input_args  # Function to retrieve command line arguments
from get_pet_labels import get_pet_labels  # Function to generate pet labels from filenames
from classify_images import classify_images  # Function to classify images using pretrained CNN
from adjust_results4_isadog import adjust_results4_isadog  # Function to adjust results to check for dogs
from calculates_results_stats import calculates_results_stats  # Function to calculate statistics
from print_results import print_results  # Function to print the results

def main():
    # TODO 0: Measure total program runtime by collecting start time
    start_time = time()

    # TODO 1: Retrieve command line arguments
    in_arg = get_input_args()  # Get arguments passed from the user in terminal
    check_command_line_arguments(in_arg)  # Check that arguments are correct

    # TODO 2: Extract pet labels from the image directory
    results = get_pet_labels(in_arg.dir)  # Extract labels based on image filenames
    check_creating_pet_image_labels(results)  # Check if labels are correctly created

    # TODO 3: Classify images using a pretrained CNN model
    classify_images(in_arg.dir, results, in_arg.arch)  # Classify images and compare labels
    check_classifying_images(results)  # Verify image classifications

    # TODO 4: Adjust results to check for correct dog classifications
    adjust_results4_isadog(results, in_arg.dogfile)  # Adjust results to account for dog breeds
    check_classifying_labels_as_dogs(results)  # Check that dog results are correctly classified

    # TODO 5: Calculate results statistics
    results_stats = calculates_results_stats(results)  # Calculate overall results and accuracy
    check_calculating_results(results, results_stats)  # Verify result calculations

    # TODO 6: Print results
    print_results(results, results_stats, in_arg.arch, True, True)  # Print final results and statistics

    # TODO 0: Measure total program runtime by collecting end time
    end_time = time()

    # TODO 0: Compute and display total runtime
    tot_time = end_time - start_time
    print("\n** Total Elapsed Runtime:", str(int((tot_time/3600)))+":"+str(int((tot_time%3600)/60))+":"+str(int((tot_time%3600)%60)))

# Call to main function to run the program
if __name__ == "__main__":
    main()
Explanation of the key sections:
Command-line Arguments (get_input_args): This part of the code retrieves and checks the command-line arguments. The script expects three arguments: the directory of images, the model architecture (e.g., vgg, alexnet, resnet), and the path to the dog breed names file.

Label Extraction (get_pet_labels): This step generates pet labels based on the filenames of the images. The assumption is that the filenames follow a specific format such as basset_hound_01034.jpg, where the breed name is included.

Image Classification (classify_images): The classify_images function uses the specified CNN architecture (such as vgg, resnet, etc.) to classify each image. The results are compared against the expected labels.

Adjusting Results for Dog Classification (adjust_results4_isadog): This function checks whether the classifier correctly identifies the pets as dogs or not. It adjusts the results if necessary, indicating whether an image was correctly classified as a dog breed.

Results Statistics (calculates_results_stats): This part computes the overall accuracy of the classification, including statistics like the percentage of correctly classified dogs and non-dogs.

Results Output (print_results): The results are printed, including the overall accuracy and the breakdown of any misclassifications (both breed-specific and dog/non-dog classifications).

Custom Functions:
get_input_args.py: Handles parsing command-line arguments.
get_pet_labels.py: Generates a dictionary of pet labels from image filenames.
classify_images.py: Classifies images using the chosen CNN model.
adjust_results4_isadog.py: Adjusts results to track if the image is classified as a dog.
calculates_results_stats.py: Computes accuracy and other statistics.
print_results.py: Prints the results and statistics.
How it Works:
Run the script: The user runs the script from the terminal with the correct arguments.
Image classification: The images are classified using the model specified by the user.
Results processing: The script adjusts results for dog classification and calculates overall accuracy.
Output: The statistics are printed to the terminal.