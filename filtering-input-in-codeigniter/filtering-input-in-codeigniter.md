---
date: 2012-12-12
---
# Filtering Input in CodeIgniter

I use CodeIgniter for my backend and have been struggling to find a good way to pass <abbr>POST</abbr> or <abbr>GET</abbr> data to its active record functions. This week I’ve found a pretty nice filtering technique I want to share with you.

Let’s start with CodeIgniter’s user guide example of inserting data.

```php
$data = array(
  'title' => 'My title',
  'name' => 'My Name',
  'date' => 'My date'
);

$this->db->insert('mytable', $data);
```

`insert` accepts two parameters. First is the table name and second is the data to insert provided as an associative array having keys as row names and values as the actual data.

The main problem is building a CodeIgniter compatible array from <abbr>POST</abbr> or <abbr>GET</abbr> data. To create it we will use the `elements` function, which is provided by CodeIgniter's `array_helper` and lets you fetch a number of items from an array. This is what I’ve come up with:

```php
$filter = array(
  'name',
  'age',
  'gender'
);

$data = elements($filter, array_filter($this->input->post(NULL, TRUE)), NULL);
$this->db->insert('person', $data);
```

At first we create a filter array defining which rows we want to be inserted. You can leave out rows which you don’t want to be influenced by user’s input provided that you’ve set up <abbr>MySQL</abbr> correctly. If any of these rows are not in the <abbr>POST</abbr> array they will be set to `NULL`, which we have defined with the third parameter of the `elements` function. This also ensures that fields in your database being set to `NOT NULL`  will throw an mysql error and the data will be refused. You could leave out the two parameters being passed to `post()` if you have globals <abbr>XSS</abbr> filtering enabled.

While this works fine for inserting data we need to add another function for updating. This is how it looks like:

```php
$filter = array(
  'name',
  'age',
  'gender'
  );
```

$data = array_filter(elements($filter, $this->input->post(NULL, TRUE)));

$this->db->where('id', $id);
$this->db->update('person', $data);</code></pre>

This time we leave out the third parameter of `elements`. Its default value is false, that’s why each data not provided by <abbr>POST</abbr>, but required by our filter array will be set to false. Afterwards we filter the result of elements with `array_filter`, a standard <abbr>PHP</abbr> function, iterating over each element of its input array and passing it to a callback function. We haven’t provided a callback which as a result removes every item with a false value `(null, false,'',0)`. As post items being always strings `NULL` and `0` will still work, but not provided data won’t be passed to the update function. To summarize only items of the filter array will be passed to the update function if any of those are provided.

I hope this could help you and I appreciate your feedback.

## UPDATE:

I’ve just recognized that you should use `array_filter` on inserts too, but in reverse order to avoid empty strings being inserted in fields which do not allow `NULL`. I’ve updated the code sample in the article.
