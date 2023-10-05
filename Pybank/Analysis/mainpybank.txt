import csv

#Reading CSV file

with open('./resources/budget_data.csv','r')as csvfile:
    csvreader= csv.reader(csvfile)

# Skipping the headers

    next(csvreader)

# Create empty list to place values in rows. Create each variable needed and start its value 

    data=[]
    total=0
    previous_profit_loss=None
    max_positive_change=None
    min_negative_change=None
    max_positive_change_date = None
    min_negative_change_date = None

# Convert data into lists 

    for row in csvreader:
        date, profit_loss = row
        profit_loss = int(profit_loss)

        data.append([date, profit_loss])

#Sum all the profit/loss values          
         
        total+= profit_loss

# Create a new column with "change" in profit/loss (diference item-previous) to calculate max and min changes

        if previous_profit_loss is not None:
            change= profit_loss - previous_profit_loss
        else:
            change=0        

        if change > 0 and (max_positive_change is None or change > max_positive_change):
            max_positive_change = change
            max_positive_change_date = date

        elif change < 0 and (min_negative_change is None or change < min_negative_change):
            min_negative_change = change   
            min_negative_change_date = date

        previous_profit_loss=profit_loss

#Calculate the number of months just getting the length of the data
    
    months = len(data)

#Define first and last value for profit/loss to calculate average. Make adjustment so denominator in average is never equal to 0

    first_value= data[0][1]
    last_value= data[-1][1]
    if (months-1) >0:
        average= (last_value - first_value)/ (months-1)
    else:
        average=0    

             
        
#Print all the information following requested format

    print ('Financial Analysis')
    print('------------------------------')
    print(f'Months: {months}')
    print(f'Total: ${total}')
    print(f"Average Change: ${average:.2f}")
    print(f'Greatest Change in Profits: {max_positive_change_date} (${max_positive_change})')
    print(f'Greatest Change in Losses:  {min_negative_change_date} (${min_negative_change})')
    




    
     












