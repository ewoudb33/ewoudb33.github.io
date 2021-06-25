---
title: "Exploring checkout data from a public library"
date: "2021-06-23"
tags: ["Exploratary Data Analysis", "SQL"]
---

When I visited my local library last weekend, I borrowed a book from the 'warehouse'. Books that aren't read that often or are too old are stocked over there. It made me think why these books are not so popular anymore and if it is possible to find out how often books are borrowed.

So I looked on the web for library data and found an interesting data source
from a public library in the United States. It includes three datasets: checkouts
data, inventory data and a dictionary to decode the checkouts information.

I will focus first on the checkouts dataset, which consists of counts by title of checkout for all physical items from 2017.

The origin of the data is a public library in Seattle, Washington. This library has 27 branches with 378,222 members. The collection consists of 2.3 million items.

I have two research questions:
- Which kind of items are checked out the most? (i.e. are the most popular)
- Can you predict which items will be checked out?

I will first explore the data by using SQL and try to answer the first question. For this occasion I used the sqldf package to be able to use SQL on dataframes in R.

First, I looked at the top 5 rows of the checkouts dataset to get a feeling of the different columns and their values.

```ruby
SELECT * FROM Library_checkouts LIMIT 5
```
<img src="{{ site.url {{ site.baseurl }}/images/top5rows_checkouts.png" alt = "">

There are 6 columns:
- Bibnumber. Corresponds to an unique item. This links to the inventory dataset which I will use later. There can be more copies of one item in the inventory.
- Itembarcode. Speaks for itself.
- ItemType. Represents the type of item that is borrowed. It links to the dictionary dataset. For example, accd represents: CD: Adult/YA.
- Collection. Represents the genre. For example, namys stands for NA-Mysteries.
- Callnumber. Item information.
- CheckoutDateTime. Moment of checkout.

One row represents one checkout in the year 2017. This dataset has
5+ million rows, so in this year were approximately 5 million checkouts.

Let's check if there are any missing values in this dataset.
```ruby
SELECT * FROM Library_checkouts WHERE BibNumber IS NULL OR ItemBarcode
      IS NULL OR ItemType IS NULL OR Collection IS NULL OR CheckoutDateTime IS
      NULL
```
The aren't any rows as an output. Therefore, we can conclude that there aren't
any missing values.

I'm interested in how many different item types and collection types there are.
Let's look it up.

```ruby
SELECT DISTINCT ItemType FROM Library_checkouts
```
```ruby
SELECT DISTINCT Collection FROM Library_checkouts
```
This shows us that there are 44 different item types and 193 different collection types.

How many items are borrowed per item type?

```ruby
SELECT COUNT(ItemType), Itemtype FROM Library_checkouts GROUP By ItemType ORDER
      BY COUNT(ItemType) DESC
```
```ruby
SELECT * FROM dictionary WHERE (Code = 'acbk' OR Code = 'jcbk' OR Code =
      'acdvd' OR Code = 'accd' OR Code = 'jcdvd')
```

The output tells us that the types Book: Adult/YA (1609307 checkouts), Book: Juvenile (1470340 checkouts), DVD: Adult/YA	(1211824 checkouts), CD: Adult/YA (431129 checkouts), DVD: Juvenile Circulating (185383) are the most popular. I looked the translation of the item types (e.g., "acbk" ) up in the dictionary dataset.

To make things more efficiently I joined the dictionary dataset with the checkouts dataset. The dictionary dataset provides information of the collection and item types.

```ruby
SELECT * FROM Library_checkouts LEFT JOIN dictionary ON  Library_checkouts.Collection = dictionary.Code
```

Then, I checked the number of borrows by collection type

```ruby
SELECT COUNT(Collection), Collection, Description FROM library_dictionary_join GROUP By Collection ORDER
      BY COUNT(Collection) DESC
```

| Number of Checkouts | Collection | Description                  |
|---------------------|------------|------------------------------|
| 757423              | nadvd      | NA-DVD, Fiction              |
| 446818              | nanf       | NA-Nonfiction                |
| 371821              | ncpic      | NC--Children's Picture Books |
| 285765              | canf       | CA-Nonfiction                |
| 220594              | cadvd      | CA3-DVD, Fiction             |
| 210451              | nafic      | NA-Fiction                   |
| 192332              | ncrdr      | NC--Children's Readers       |
| 186942              | nacd       | NA-Compact Discs             |
| 150925              | ncdvd      | NC-Children's DVDs           |
| 149371              | ncfic      | NC-Children's Fiction        |

DVDs are on top, but it is misleading. There are probably many book categories, because the item type Book: Adult/YA ranked higher in the previous output. Interesting to see is that non fiction for New Adults (NA) seems to be more popular than fiction books. Moreover, children's categories ranks quite high in this Library. Other popular book fictional book genres are: NC-Easy Fiction (91673 checkouts), NA-Mysteries (72168 checkouts), NA-Sci-Fic/Fantasy (32019 checkouts). Less popular fictional book genres are: NA-Westerns (657 checkouts) and NA-Short Stories (308 checkouts).

Which items are the most popular in this library in 2017? I used the following query to get an answer.

```ruby
SELECT COUNT(BibNumber) AS number_of_checkouts, BibNumber, Description
FROM library_dictionary_join GROUP BY BibNumber ORDER BY COUNT(BibNumber) DESC
```

The output of this query doesn't give any information of the item, but only a number. To get more information, I merged the inventory dataset with the checkout data. The Inventory dataset gives detailed information about the items such as the Author, Title etc.

```ruby
SELECT * FROM books_borrowed LEFT JOIN inventory ON books_borrowed.BibNumber = inventory.BibNum
```
<img src="{{ site.url {{ site.baseurl }}/images/popular_items_library.png" alt = "">

The most borrowed item is, surprisingly enough, an SPL HotSpot. The seattle library offers to loan Wi-Fi access with your library card.

The third and fourth place are both movies: Arrival and Moonlight.

On the 5th place is the highest ranked book: The Underground Railroad : a novel by Colson Whitehead. This book was published in 2016, one year before this dataset was created. Other high ranked novels where often published in 2016 or 2017. It seems that date of publication could correlate with checkouts. This can
be a good variable in our machine learning model.

Let's see which authors are the most popular.

```ruby
SELECT sum(number_of_checkouts), Author FROM books_borrowed_details GROUP BY Author ORDER BY sum(number_of_checkouts) DESC
```

| Number of Checkouts | Author             |
|---------------------|--------------------|
| 26645               | Willems, Mo        |
| 17029               | Seuss, Dr.         |
| 16820               | Stilton, Geronimo  |
| 16305               | Davis, Jim,        |
| 14945               | Meadows, Daisy     |
| 11712               | Holm, Jennifer L.  |
| 11071               | Osborne, Mary Pope |
| 9792                | Arnold, Tedd       |
| 9782                | Patterson, James   |
| 9593                | Pilkey, Dav        |

Author's of children's books are quite popular in this library: 8 out of 10 are writing children's literature.

I also looked up two of my favourite Authors. You might remember Martin Booth from the previous article, where I looked up the review data. Lets see if he is popular in Seattle.

```ruby
SELECT * FROM books_borrowed_details WHERE Author LIKE
'Christie%'
```

| Number of Checkouts | Title                         |
|---------------------|-------------------------------|
| 104                 | Murder on the Orient Express  |
| 84                  | And then there were none      |
| 59                  | Crooked house                 |
| 44                  | After the funeral             |
| 39                  | Sad cypress                   |
| 39                  | Taken at the flood            |
| 38                  | The secret adversary          |
| 36                  | The mystery of the Blue Train |
| 35                  | The murder of Roger Ackroyd   |
| 34                  | 4:50 from Paddington          |

```ruby
SELECT * FROM books_borrowed_details WHERE Author LIKE
'%Booth, Martin%'
SELECT * FROM Library_checkouts WHERE BibNumber =
                           2678556 OR BibNumber = 2218916
```
That isn't the case. 'A very private gentleman', there are two copies in the inventory, was only read 3 times in 2017. Below you can see the three
transactions.

<img src="{{ site.url {{ site.baseurl }}/images/transactions_avpg.png" alt = "">

And the murder on the Orient Express is the most popular Agatha Christie's.

After this analysis I have quite a good feeling of this data. Next time I might try machine learning to predict book checkouts.
