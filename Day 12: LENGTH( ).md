## Day 12: LENGTH()

The SQL CHAR_LENGTH() function returns the number of characters in a given string. This function counts every character, including spaces, special characters, and punctuation marks. It is useful for validating input lengths, analyzing string data, or performing quality checks on text fields.

### Syntax:

```sql
SELECT LENGTH(string) ; 
```

• string: The input string whose byte length is to be determined. 

### Key Difference from CHAR_LENGTH(): 

• CHAR_LENGTH() counts the number of characters in a string. 
• LENGTH() counts the number of bytes. For single-byte character sets like ASCII, both functions return the same value. For multi-byte character sets like UTF-8, it may return a larger number. 

### Example:

The following example calculates the length of the string ' Hello World! '.

```sql
SELECT 
 'Hello World!' AS Text, 
 LENGTH('Hello World!') AS ByteLength;
```

| Text         | ByteLength | 
|--------------|------------|
| Hello World! |   12       | 

### Question:

### Problem Statement

You are managing a database for a content platform where users submit articles.The `articles` table contains the following columns:  

| Column Name   | Data Type     | Description                 |  
|---------------|---------------|-----------------------------|  
| article_id    | INT           | Unique ID for each article  |  
| title         | VARCHAR(255)  | Title of the article        |  
| content       | TEXT          | Main content of the article |  
| language      | VARCHAR(20)   | Language of the article     |  

Task:
1. Identify articles:  
   • Where the title length in bytes exceeds 10 bytes.  
   • Where the content length in bytes exceeds 80 bytes.  
2. Additionally, categorize these articles by language to see if specific languages tend to have longer titles or content.  
3. Display the following in the result:  
   • language  
   • Number of articles with long titles (title > 10 bytes)  
   • Number of articles with long content (content > 80 bytes)   
   
### Schema setup

```sql
CREATE TABLE articles (
    article_id INT,
    title VARCHAR(255),
    content TEXT,
    language VARCHAR(20)
);

INSERT INTO articles (article_id, title, content, language) VALUES
(1, 'A Journey Through Time', 'This is a sample content. ', 'English'),
(2, '科技的未来', '未来的科技将改变我们的生活。', 'Chinese'),
(3, 'Exploring the Universe', 'Space exploration is a fascinating field.' , 'English'),
(4, 'Historia y Cultura', 'La historia de la humanidad es vasta y compleja. ', 'Spanish'),
(5, '现代生活的挑战', '现代社会面临着各种挑战，包括技术和社会问题。', 'Chinese'),
(6, 'The Evolution of Language', 'Language evolves over time, reflecting cultural changes. ', 'English'),
(7, 'Arte y Sociedad', 'El arte es una expresión de la sociedad. ', 'Spanish'),
(8, '技术与创新', '技术创新对经济发展起着重要作用。', 'Chinese');
```

### Expected output

| Language  | Long_Title_Count | Long_Content_Count |  
|-----------|------------------|--------------------|  
| English   | 3                | 0                  |  
| Chinese   | 3                | 3                  |  
| Spanish   | 2                | 0                  |  

### Solution Query

```sql
SELECT 
    language,
    SUM(CASE WHEN LENGTH(title) > 10 THEN 1 ELSE 0 END) AS Long_Title_Count,
    SUM(CASE WHEN LENGTH(content) > 80 THEN 1 ELSE 0 END) AS Long_Content_Count
FROM articles
GROUP BY language;
```
