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

*next step*
after cleaning the dataset now ready for the loading part setup the postgres and add the columns to the postgres.
