# PyPoll-Challenge
1.	Overview of Election Audit: Explain the purpose of this election audit analysis.

	This election audit was designed to count each vote that each candidate received, and the total vote of each county included in the election. These tallies were used to conduct a basic analysis of vote share by candidate and by county, then to output the results in a text file.

2.	Election-Audit Results: Using a bulleted list, address the following election outcomes. Use images or examples of your code as support where necessary.
o	How many votes were cast in this congressional election?
<img width="297" alt="Total Votes" src="https://user-images.githubusercontent.com/90073490/135927053-7443fe6d-bb59-4a91-baa7-0f9961d80ca0.png">
o	Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.
<img width="600" alt="County Votes" src="https://user-images.githubusercontent.com/90073490/135927315-91f07f7d-e00f-4ab9-9c49-7448f01af4b3.png">
o	Which county had the largest number of votes?
<img width="333" alt="Largest Turnout" src="https://user-images.githubusercontent.com/90073490/135927336-c15c44d7-1114-456e-bfb2-81650e121701.png">
o	Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.
<img width="331" alt="Candidate Vote Share" src="https://user-images.githubusercontent.com/90073490/135927359-5c0d1b2f-cd1e-420d-b7a9-b46faedc4e58.png">
o	Which candidate won the election, what was their vote count, and what was their percentage of the total votes?
<img width="313" alt="Election Winner" src="https://user-images.githubusercontent.com/90073490/135927372-eb90f49f-a2ec-4167-b984-24e5d9e094ec.png">
3.	Election-Audit Summary: In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at least two examples of how this script can be modified to be used for other elections.

  This script could be easily generalized for use in any election where the input data contains which candidate each vote was cast for, and which county the vote was cast in. There is no hardcoded county list or candidate list, which means that each new data set will generate new and relevant lists of candidates and counties. Furthermore, this script can run with any number of unique counties and candidates, and where the number of votes is limited only by the processing power of the computer.
  
	That being said, there are a couple of modifications which would make the script more usable across a wider range of election scenarios. The code is only able to count votes according to the county in which they were cast. If the election officials wanted to include more specific geographic information and have it analyzed according to a different geospatial unit, the code would require modification. I would recommend inserting a nested for loop to check columns marked with geographic information and analyze each column individually.
  
	Second, while the script analyzes votes by county and by candidate, it does not do both simultaneously. It is not currently possible to view the vote within a particular geographic area. This functionality could be added using a nested dictionary to store the votes for a particular candidate within a particular county. Adding a vote for a candidate would then add it to the compartment  corresponding to the correct county dictionary and candidate.
<img width="897" alt="Screen Shot 2021-10-04 at 3 31 01 PM" src="https://user-images.githubusercontent.com/90073490/135927613-f5b2ba16-dcf8-4cfe-b76c-daccd7347e26.png">

CODE:

# -*- coding: UTF-8 -*-
"""PyPoll Homework Challenge Solution."""

# Add our dependencies.
import csv
import os

# Add a variable to load a file from a path.
file_to_load = os.path.join("/Users/jaredschwartz/Downloads/Resources", "election_results.csv")
# Add a variable to save the file to a path.
file_to_save = os.path.join("/Users/jaredschwartz/Downloads/Resources", "election_analysis.txt")

# Initialize a total vote counter.
total_votes = 0

# Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

# 1: Create a county list and county votes dictionary.
county_list = []
county_votes = {}

# Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

# 2: Track the largest county and county voter turnout.
largest_county_turnout = ""
highest_turnout = 0

# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county_list:

            # 4b: Add the existing county to the list of counties.
            county_list.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1


# Save the results to our text file.
with open(file_to_save, "w") as txt_file:

    # Print the final vote count (to terminal)
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n"
        f"County Votes:\n\n")
    print(election_results, end="")

    txt_file.write(election_results)

    # 6a: Write a for loop to get the county from the county dictionary.
    for county in county_list:
        
        county_results = (
        # 6b: Retrieve the county vote count.
        # 6c: Calculate the percentage of votes for the county.
        f"{county}: {((county_votes[county]/total_votes)*100):.1f}% ({county_votes.get(county):,}) "

        # 6d: Print the county results to the terminal.
        f"\n"
        )
        print(county_results, end="")
         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)

         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (county_votes[county]/total_votes) >= (highest_turnout/total_votes):
            highest_turnout = county_votes[county]
            largest_county_turnout = county


    # 7: Print the county with the largest turnout to the terminal.
    top_turnout = (f"\n"
    f"The county with the largest turnout is {largest_county_turnout} with {highest_turnout:,} votes and {((highest_turnout/total_votes)*100):.1f}% turnout."
    f"\n"
    f"-------------------------\n\n")
    print(top_turnout, end="")

    # 8: Save the county with the largest turnout to a text file.
    txt_file.write(top_turnout)

    # Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        # Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
        txt_file.write(candidate_results)

        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

    # Print the winning candidate (to terminal)
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)

    # Save the winning candidate's name to the text file
    txt_file.write(winning_candidate_summary)
