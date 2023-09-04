1. import the necessary libraries (numpy, pandas,seabornand matplotlib.pyplot)
2. read the dataframe using pd.read_csv(r'') and the right file path
3. df.tail()...reads the dataset from the bottom.
4. df.shape...gives the number of columns and rows in the dataset.
5. Check for missing values using:df.isnull().sum()...and after running this code, you realize 'City' has 16 missing values which needs to taken care of before you tontinue to analyze the dataset. 
6. perform thorough data cleaning to get good results. Convert the($), (M) and (B) to integers and change the 'Date Joined' and 'Year Founded' to Datetype format and finally convert the 'Valuation' and 'Funding' columns to integers. 
7. Run this code to do the conversion andother cleaning aswell.
def convert_to_number(x):
    if x[-1] == 'M':
        return float(x[:-1])* 1e6
    elif x[-1] == 'B':
        return float(x[:-1])* 1e9
    else:
        return x
    
df['Valuation'] = df['Valuation'].astype(str).str.replace('$', '').apply(convert_to_number).astype(float)

df['Funding'] = df['Funding'].replace('unknown', '0').str.replace('$', '').str.replace('M', '000000').str.replace('B', '000000000').replace('Unknown', '0').apply(convert_to_number).astype(float)

df.head()
8. USe df.dtypes to check the data types,ex; float, Int,etc
9. convert the Date Joined to Datetype format using this code.

df['Date Joined'] = pd.to_datetime(df['Date Joined'])
df['Year Founded'] = pd.to_datetime(df['Year Founded'], format = '%Y')

10. Check the updated dataFrame using df.head()
11. And then run this code to calculate the age the company joined and will add a new column to the dataframe:

df['Age of Joining'] = ((df['Date Joined'] - df['Year Founded']).dt.days / 365).round(1)

df.head()

12.Apply the FFill method to the 'City' and 'Select Investment' columns usinfg df.isnull().sum()to fill forward every null value. 
13. Check updated table for missing values and plot a heat map to visualize it. 
14. Perform a univariate, bivariate and multivariate analysis.
15. Start with the Univariate Analysis by analysing the Industry per Company count using this code:
Ind_count = df['Industry'].value_counts().sort_values(ascending = True)
Ind_count

16. Perfrom a Bivariate Analysis by analysing using distribution of Valuation by Country using this code: 
df.groupby('Industry')['Funding'].value_counts().astype('string').sort_values(ascending = True)

17.Visualize using boxplot to be able to red the median values. 
18.I performed other bivariate analysis, and thats preferancial depending on what excatly you want to analyze/
19.The next Analysis was multivariate analysis where i visaulized using the correlation matrix and a grid of scatter plot and also a visualization of the numerical values in a barplot

20.I began to do the main analysis starting with which companies have the biggest return on investment. To calculate the ROI fo each company,you must "deduct Funding Values from Valuation values and then divide by Funding". Usin gthe code below:
df['ROI'] = (df['Valuation'] - df['Funding']) / df['Funding']
df['ROI']
with df as the dataframe and ROI as the variable for return on investment.
After that i sorted it down to the top 10 companies for easy analysis.Using this code below: 

top_10_companies = df.head(10)
top_10_companies

after sorting i visualized it with a bar chat. 
21. The second analysis is "How long does it usually take for a company to become a unicorn? Has it always been this way?"
- First have to convert the Year Founded column to datetime, 
- then calculate the time taken for a company to be a unicorn by multiplying Valuation by itself and then deducting Year Founded by sorting with "int", "min", "cumsum".
- the following step is to Calculate the median time taken for a company to become a unicorn by calculating the median of time to unicorn variable. 
- the next step is to Group the data by year and calculate the median time taken for a company to become a unicorn each year, using this code: 
yearly_median_time_to_unicorn = df.groupby(df['Year Founded'].dt.year)['Time_to_Unicorn'].median()
yearly_median_time_to_unicorn
- then sort the values to the top 10 and then visualize them using a line plot.
- After ,Compare the yearly median times to the overall median time by deducting median_time_to_unicorn from yearly_median_time_to_unicorn.
- Visualize using a bar chart. 

22. the following Analysis was "Which countries have the most unicorns? Are there any cities that appear to be industry hubs?"
- first group the dataset by 'Country' and then count the number of unicorns in each country in descending order
- the next time is to sort the values to top 10
- Visualize using bar chart. 
- the second part of the analysis is to find the cities that appear to be industry hubs by grouping the data by city and count the number of unicorn companies in each city.
- After this, visualize using a barchart. 

22.finally i analyzed Which investors have funded the most unicorns?
- first call investor_count using the Select Investor colum from the dataframe and then sort to top 5. 
- then visualize using a bar chart. 

The major challenges i faced was my inabilty to convert the "M", "B" and "$" signs and values to integers. As a beginner, i found it very intimidating an stressful until after a few days of researching and asking questions all through trails and errors, i finally got help to go through it and it worked. 
The second challenge faced was the fact that, i didnt even know what to search when using the Ai assistant. I believe there is some level of knowledge and understanding that on needs before embarking on any journey. without these tools, it is impossible to even ask the right questions because you have no idea of what you are doing. 
Overall, i would say this assignment has opened me up to the many possibilities using python and the need to still fight on in the learning, un-learning and re-learning process. 
