# LiveProject-CodeSummary
Code Summary of Python/Django Live-Project

## Introduction
I was part of a Live project for the last two weeks, where we used Python with the Django Framework to build websites. The cool thing about this project was we utilized
Agile methodologies and daily Scrums. I learned the logistics behind coding with other developers, utilizing version control by branching and making pull requests with master and most importantly, I learned front end and back end development and also with rendering API data to my templates.

## CRUD Functionality
Create, Read, Update & Delete; the basics of development. These were part of the beginning stories with our Project, and although seemingly simple, they do teach you the fundamentals of Software.

### Create
    Here we created models in Django as an internal database table and also render a form on a template for a user to create an instance of that model!

    from django.db import models

    class AddBook(models.Model):
        book_genre = models.CharField(max_length=20, choices=BOOK_GENRE)
        book_title = models.CharField(max_length=100, null=False)
        book_author = models.CharField(max_length=100, null=False)
        book_description = models.CharField(max_length=100, null=False)
        book_rating = models.CharField(max_length=20, choices=BOOK_RATING)

    objects = models.Manager()

### template

    {% extends "Books/Books_Base.html" %}

    {% load crispy_forms_tags %}

    {% load static %}

    {% block title %} Add a Book{% endblock %}


    {% block content %}
    <h1 class="fancy">Create a Review</h1>
    <div class="add-book-container">
        <form method="POST" class="add-book-form">
            {% csrf_token %}
            {{ form|crispy }}
            <br>
            <button class="btn btn-success" type="submit" name="Save_Review">Submit</button>
        </form>
    </div>

    {% endblock %}

### View Function to Render form to template

    def books_add_book(request):
        form = AddBookForm(data=request.POST or None)
        if request.method == 'POST':
            if form.is_valid():
                form.save()
                return redirect('books_reviews')
        content = {'form': form}
        return render(request, 'Books/Books_AddBook.html', content)

