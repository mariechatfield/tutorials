---
layout: tutorial
title:  "Firebase | Step 2: Write data manually in the Firebase Dashboard"
tutorial_overview: firebase
previous_step: step1.html
next_step: step3.html
---
## BEFORE

| You should... | What to Review |
|------------ |-------- |
| ...be looking at your project's Database console.| [Step 1](step1.html) |
| ...know **your-project-id**, the unique description of your database.| [Step 1](step1.html) |

## DURING

Right now, your database is pretty empty. All it contains is a reference to your database (**your-project-id**), which points to a null (empty) object.

![My First App Dashboard]({{site.baseurl}}/assets/firebase/screenshot_empty_db.png)

Everything in Firebase is organized in a hierarchy under this starting reference, as a single JSON object with other JSON objects and data nested inside it.

| ![Pause Point]({{site.baseurl}}/assets/firebase/pause_point.png) | [What is JSON?]({{ site.baseurl }}/explanations/json.html) |
| --- | --- |

Let's add some data. For now, we just want to keep track of who is maintaining this database. We can think of this as an array of names:

![Maintainers list diagram]({{site.baseurl}}/assets/firebase/diagram_app_maintainers.png)

```json
"maintainers": [
    "marie",
    "femmehacks"
]
```

`maintainers` is the name of our array. It belongs at the top level of our database, as a key of **your-project-id**. We can manually add this list in the Firebase Dashboard by pressing the green plus next to **your-project-id**.

Don't see the green plus? You may need to hover your mouse over **your-project-id** to make the edit box appear. When you do, you should see a new row appear with two empty text boxes: one for **name** and one for **value**.

![Adding data manually]({{site.baseurl}}/assets/firebase/screenshot_add_data.png)

For **name**, add the key: ```maintainers```

For **value**, add the entire value object: ```["marie", "femmehacks"]```

Make sure that you use quotes (```"```) around each name in your value object.

![Adding maintainers information]({{site.baseurl}}/assets/firebase/screenshot_add_maintainers.png)

Once we save the new data (by clicking the blue **ADD** button), we can see that the maintainers list is now in our database! The box might show up with a green highlight at first, indicating that the data has just been added.

![Saved maintainers list]({{site.baseurl}}/assets/firebase/screenshot_save_maintainers.png)

If you click on **maintainers**, you should be directed to __https://console.firebase.google.com/project/your-project-id/database/data/maintainers__.

![Maintainers dashboard]({{site.baseurl}}/assets/firebase/screenshot_database_maintainers.png)

Instead of seeing the entire database, this Dashboard allows us to inspect only the **maintainers** object of our database, and any nested data.

### EXTRA CREDIT

1. Add another name to the **maintainers** array
2. Edit a name in the **maintainers** array
3. Delete a name from the **maintainers** array
4. Add another object to the top level of **your-project-id**
5. Figure out what URL you would need to link directly to one of the names in the **maintainers** array

## AFTER

You can edit, add, or delete data manually from your project's Database console.

You can link directly to a nested object in your project's database.

*Be careful manipulating data through your project's Database console once you populate your database with real data!* You don't want to accidentally ruin or delete the data that makes your application useful to users.

**Step 3:** [Write hard-coded data via the Javascript Library](step3.html)
