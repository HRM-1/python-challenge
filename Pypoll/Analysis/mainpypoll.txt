import csv

#Create an empty dictionary to count the votes

votes_count={}

#Reading the csv file

with open('./resources/election_data.csv','r')as csvfile:
    csvreader= csv.reader(csvfile)

#Skip header to focus on data

    next(csvreader)        
    
#Start variable  
    
    total_votes=0

 #Iterate and count  
    
    for row in csvreader:
        ID, county,candidate_name = row
        total_votes+=1
        
        if candidate_name in votes_count:
            votes_count[candidate_name] +=1

        else:
            votes_count[candidate_name]=1


    print ('Election Results')
    print('----------------------')
    print(f'Total Votes: {total_votes}')
    print('----------------------')
    print("Total Votes per Candidate:")

#Create Variables to calculate totals per candidate, percentage of votes and winner

    max_votes =0
    winner=""

    for candidate,votes in votes_count.items():
        print(f'{candidate}:{(votes/total_votes) * 100:.3f}% ({votes})')
        if votes> max_votes:
            max_votes=votes
            winner=candidate
    print('----------------------')
    print(f'Winner:{winner}')
    print('----------------------')