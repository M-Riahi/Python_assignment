# Python_assignment
import csv

# Variables
total_months = 0
total_net = 0
monthly_change = []
month_count = []
greatest_increase = 0
greatest_increase_month = 0
greatest_decrease = 0
greatest_decrease_month = 0

# Set Path For File
csvpath = os.path.join('..', 'Resources', 'budget_data.csv')

# Open & Read CSV File
with open(csvpath, newline='') as csvfile:
    
    # CDelimiters identification
    csvreader = csv.reader(csvfile, delimiter=',')
    
    # Read The Header Row First & (Skip This Step If There Is No Header)
    csv_header = next(csvreader)
    first_row = next(csvreader)
    
    # Cal: Total Number Of Months, Net Amount Of "Profit/Losses" and Set Variables For Rows
    previous_row = int(first_row[1])
    total_months += 1
    net_amount += int(first_row[1])
    greatest_increase = int(row[1])
    greatest_increase_month = row[0]
    
    # Row reader after header
    for row in csvreader:
        
        # Cal: Total Number Of Months Included In The data
        total_months += 1
        # Calculate Net Amount Of "Profit/Losses" Over The Entire Period
        net_amount += int(row[1])

        # Cal: Change From Current Month To Previous Month
        revenue_change = int(row[1]) - previous_row
        monthly_change.append(revenue_change)
        previous_row = int(row[1])
        month_count.append(row[0])
        
        # Cal: The Greatest Increase
        if int(row[1]) > greatest_increase:
            greatest_increase = int(row[1])
            greatest_increase_month = row[0]
            
        # Cal: The Greatest Decrease
        if int(row[1]) < greatest_decrease:
            greatest_decrease = int(row[1])
            greatest_decrease_month = row[0]  
        
    # Cal: The Average & The Date
    average_change = sum(monthly_change)/ len(monthly_change)
    
    highest = max(monthly_change)
    lowest = min(monthly_change)

# Print in reserve data set
print(f"Financial Analysis")
print(f"---------------------------")
print(f"Total Months: {total_months}")
print(f"Total: ${net_amount}")
print(f"Average Change: ${average_change:.2f}")
print(f"Greatest Increase in Profits:, {greatest_increase_month}, (${highest})")
print(f"Greatest Decrease in Profits:, {greatest_decrease_month}, (${lowest})")

# output source
output_file = os.path.join('..', 'Resources', 'budget_data_revised.text')

# Open File with "Write" Mode while specifying variables holding centent
with open(output_file, 'w',) as txtfile:

# Write New Data
    txtfile.write(f"Financial Analysis\n")
    txtfile.write(f"---------------------------\n")
    txtfile.write(f"Total Months: {total_months}\n")
    txtfile.write(f"Total: ${net_amount}\n")
    txtfile.write(f"Average Change: ${average_change}\n")
    txtfile.write(f"Greatest Increase in Profits:, {greatest_increase_month}, (${highest})\n")
    txtfile.write(f"Greatest Decrease in Profits:, {greatest_decrease_month}, (${lowest})\n")
