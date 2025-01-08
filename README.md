*for this analysis i could have done the review and user name but my need was to analytic the product detials so i choosed to drop the review and user name and keep the necessary details*
for the review you can use 
```python
data['user_name'] = data['user_name'].str.split(',')
data['user_id'] = data['user_id'].str.split(',')
data['review_id'] = data['review_id'].str.split(',')
data['review_title'] = data['review_title'].str.split(',')
```
this is the executive line for spliting.

```python
data_separate = data.explode('user_id')
data_separate['user_name'] = data_separate['user_name'].explode().reset_index(drop= True)
```
explode is used to split the details and place it like a row eg
a: [1,2]
b:['sujan','rai''
[1: 'sujan' 2:'rai''

```python
data_separate['review_id'] = data_separate['review_id'].explode().reset_index(drop=True)
data_separate['review_title'] = data_separate['review_title'].explode().reset_index(drop=True)
data_separate['review_content'] = data_separate['review_content'].explode().reset_index(drop=True)
```
same goes for this code

this is helpful if you want to get the proper focusing on user and review 

although it might see easy but after splitting with the review content there would be several line review you need to convert into the spliting which take good understanding of the python one 
```python
data = {'review_content': [
    "Looks durable Charging is fine tooNo complains,Charging is really fast, good product.,Value for money",
    "I ordered this cable to connect my phone to Android Auto of car. The cable is really strong and ...",
    "Not quite durable and sturdy,Working good,Product,Very nice product,Working well,It's a really nice product"
    # Add all your review content here
] * 488}  # Replicating for example purposes (3 * 488 = 1,464)

df = pd.DataFrame(data)

df['review_content'] = df['review_content'].str.split(',')
df_exploded = df.explode('review_content')

df_exploded['review_content'] = df_exploded['review_content'].str.strip()

df_cleaned = df_exploded[
    ~df_exploded['review_content'].str.startswith('http') &  # Remove URLs
    df_exploded['review_content'].str.len() > 0             # Remove empty strings
]

df_cleaned = df_cleaned.drop_duplicates()

df_cleaned.to_csv("cleaned_reviews.csv", index=False)

print(df_cleaned.head())
print(f"Total reviews processed: {df_cleaned.shape[0]}")
```
 you need to add all the content of review content in the code

*next step*
after cleaning the dataset now ready for the loading part setup the postgres and add the columns to the postgres.
