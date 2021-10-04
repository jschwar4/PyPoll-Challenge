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
