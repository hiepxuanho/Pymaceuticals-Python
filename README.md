# Pymaceuticals-Python
Applying what I learned about Matplotlib to a real-world situation and dataset. 


I got confused at the instruction "Our data should be uniquely identified by Mouse ID and Timepoint". I did know that we definitely needed to use duplicate() function, but I had no idea how to return the right result since the data should be uniquely indentified both Mouse ID and Timepoint. 

After getting explanation from the professor, I realize that inorder to identify duplicate rows where the combination of Mouse ID and Timpoint shows up more than once. However, I only knew how to use duplicated() function with one condition.

Therefore I had to look up on Chat GPT on how to solve this question. It gave me the result of using duplicated() function with a subset = ["Mouse ID", "Timepoint"]. In this way, we can find the duplicate not only on Mouse ID but also Timepoint as well.

/------------Chat GPT code---------------------------/

duplicate_mice = mouse_study_complete[mouse_study_complete.duplicated(subset=['Mouse ID', 'Timepoint'], keep=False)]

/----------------------------------------------------/

And for us to find the duplicate mice by ID number, we had to use unique() function on the duplicate mouse data we just found by using duplicated().

/------------Chat GPT code---------------------------/

duplicate_mouse_ids = duplicate_mice['Mouse ID'].unique()

/----------------------------------------------------/

I had to look up Chat GPT to find out what function to drop a specific Mouse ID. It gave me the solution with function isin() which was very new to me. This eventually returned a correct answer.

/------------Chat GPT code---------------------------/

cleaned_mouse_data = mouse_study_complete[~mouse_study_complete['Mouse ID'].isin(duplicate_mouse_id)]

/----------------------------------------------------/
