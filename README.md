# Python-NumPy
Learn Python NumPy Deep Dive

### What is Numpy in Python?
NumPy, which stands for "Numerical Python," is a fundamental Python library for numerical and scientific computing. It provides support for working with large, multi-dimensional arrays and matrices of data, as well as a collection of mathematical functions to operate on these arrays efficiently. NumPy is a crucial tool for various scientific and engineering applications, including data analysis, machine learning, and scientific research.

Key features of NumPy include:

1. **Multi-dimensional Arrays:** NumPy's primary data structure is the `numpy.ndarray`, which is an efficient, homogeneous array that can store elements of the same data type. These arrays can have multiple dimensions, making it suitable for tasks involving vectors, matrices, and higher-dimensional data.

2. **Array Operations:** NumPy provides a wide range of mathematical and logical functions for performing operations on arrays. These operations can be performed element-wise, making it highly efficient for tasks like element-wise addition, subtraction, multiplication, and more.

3. **Broadcasting:** NumPy has a broadcasting feature that allows operations on arrays with different shapes and dimensions, making it more flexible and powerful for data manipulation.

4. **Integration with other Libraries:** NumPy integrates well with other Python libraries used for scientific and data analysis, such as SciPy (scientific computing), Matplotlib (data visualization), and scikit-learn (machine learning).

5. **Efficiency:** NumPy is implemented in C and Fortran, which makes it significantly faster than standard Python lists for numerical computations. It also supports vectorized operations, which can be much more efficient than equivalent operations using standard Python loops.

To use NumPy, you typically need to import it into your Python code, like this:

```python
import numpy as np
```
### NumPy Programs

**Program 1: Hello, World!**
This classic program simply prints "Hello, World!" to the console.

```python
print("Hello, World!")
```

**Program 2: Calculate the Area of a Circle**
This program calculates the area of a circle based on the radius entered by the user.

```python
import math

# Get the radius from the user
radius = float(input("Enter the radius of the circle: "))

# Calculate the area
area = math.pi * (radius ** 2)

# Print the result
print(f"The area of the circle with radius {radius} is {area:.2f}")
```

### NumPy Project

**Project Description:**

Create a web-based to-do list application using Python, along with a web framework like Flask or Django for the backend and HTML/CSS/JavaScript for the frontend. This project will help you learn about web development, databases, and how to create interactive web applications.

**Key Features:**

1. **User Authentication:** Allow users to sign up, log in, and log out. Each user should have a personal to-do list.

2. **To-Do List Management:**
   - Users can add tasks to their to-do list.
   - Mark tasks as completed.
   - Edit and delete tasks.
   - Prioritize tasks with due dates and labels.

3. **Data Storage:** Store user accounts and to-do lists in a database. You can use an SQL database (e.g., SQLite, PostgreSQL) or a NoSQL database (e.g., MongoDB).

4. **User-Friendly Interface:** Create a user-friendly web interface for adding, editing, and managing tasks. You can use HTML, CSS, and JavaScript for this.

5. **Notifications:** Implement email or in-app notifications for upcoming tasks or reminders.

6. **Search and Filter:** Add a search and filter feature to easily find tasks based on keywords or labels.

7. **Security:** Ensure secure user authentication and data storage. Implement password hashing and validation to protect user data.

8. **Responsive Design:** Make your web app responsive, so it works well on both desktop and mobile devices.

**Additional Challenges:**

- **Mobile App:** After completing the web app, you can create a mobile app version using a framework like React Native or Flutter.
- **Cloud Deployment:** Deploy your web app on a cloud platform like Heroku or AWS.
- **Collaboration:** Add the ability for users to share lists and collaborate on tasks.
### ---------------------------------------------------------------------------------
### Project Code
Creating a full-fledged project like a to-do list web app is a substantial endeavor, and providing the entire code here would be extensive. However, I can give you an outline of the steps to get started, and you can find resources and tutorials online to guide you through the implementation.

Here's a simplified structure of how you might approach building a to-do list web app using Flask (a Python web framework) as a starting point:

**1. Setting Up the Environment:**

First, ensure you have Python and Flask installed. You can install Flask using `pip`:

```bash
pip install Flask
```

**2. Create Project Structure:**

Organize your project with folders for templates (HTML files), static files (CSS, JavaScript), and a main application file:

```
my_todo_app/
    app.py
    templates/
        index.html
    static/
        style.css
```

**3. Build the Web Application:**

- In your `app.py` file, set up the Flask application, define routes, and handle user authentication.
- Create HTML templates for registration, login, and the to-do list interface.
- Implement data storage using a database (e.g., SQLite for simplicity or a more robust option like PostgreSQL).

Here's a simplified example of `app.py`:

```python
from flask import Flask, render_template, request, redirect, url_for
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///todos.db'
db = SQLAlchemy(app)

# Define the database model for tasks
class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(200), nullable=False)
    completed = db.Column(db.Boolean, default=False)

# Create database tables
db.create_all()

# Define routes and functions to handle tasks

@app.route('/')
def index():
    tasks = Task.query.all()
    return render_template('index.html', tasks=tasks)

@app.route('/add_task', methods=['POST'])
def add_task():
    content = request.form['content']
    new_task = Task(content=content)
    db.session.add(new_task)
    db.session.commit()
    return redirect('/')

@app.route('/complete_task/<int:id>')
def complete_task(id):
    task = Task.query.get(id)
    task.completed = True
    db.session.commit()
    return redirect('/')

# ... Add more routes for editing, deleting tasks, user authentication, etc.

if __name__ == '__main__':
    app.run(debug=True)
```

**4. Create HTML Templates:**

Design the frontend by creating HTML templates in the `templates` folder. Here's a basic example of `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My To-Do List</title>
    <link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>My To-Do List</h1>
    <form method="POST" action="/add_task">
        <input type="text" name="content" placeholder="Add a task" required>
        <button type="submit">Add</button>
    </form>
    <ul>
        {% for task in tasks %}
        <li {% if task.completed %}class="completed"{% endif %}>
            {{ task.content }}
            <a href="/complete_task/{{ task.id }}">Complete</a>
        </li>
        {% endfor %}
    </ul>
</body>
</html>
```

**5. Styling:**

You can add CSS in the `static/style.css` file to style your web app.

Certainly! Here's a simple CSS code snippet that you can use in your `static/style.css` file to style your to-do list web app:

```css
/* Reset some default styles */
body, ul {
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    color: #333;
}

h1 {
    text-align: center;
    padding: 20px;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin: 10px 0;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

li.completed {
    background-color: #d3f8e2; /* Light green for completed tasks */
}

li a {
    color: #e74c3c; /* Red for delete links */
    text-decoration: none;
    margin-left: 10px;
}

li a:hover {
    text-decoration: underline;
}

form {
    text-align: center;
    padding: 20px;
}

input[type="text"] {
    width: 70%;
    padding: 5px;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin-right: 10px;
}

button[type="submit"] {
    background-color: #3498db;
    color: #fff;
    border: none;
    border-radius: 5px;
    padding: 5px 15px;
    cursor: pointer;
}

button[type="submit"]:hover {
    background-color: #2980b9;
}

/* Media query for smaller screens */
@media (max-width: 600px) {
    li {
        flex-direction: column;
    }

    li a {
        margin-top: 10px;
    }
}
```

This CSS code includes styles for the to-do list items, the form for adding tasks, and responsive design adjustments for smaller screens. You can modify and customize these styles to fit your design preferences.

### ---------------------------------------------------------------------------------
### How to check Python Flask in my desktop ?
To check if Python and Flask are installed on your desktop, follow these steps:

**1. Check Python Installation:**

First, ensure that Python is installed on your desktop. Open a terminal or command prompt and type the following command:

```bash
python --version
```

This command should display the installed Python version. If you see an error or if Python is not installed, you'll need to download and install Python. You can download Python from the official Python website: https://www.python.org/downloads/

**2. Check Flask Installation:**

Once you've verified that Python is installed, you can check if Flask is installed. To do this, open your terminal or command prompt and run the following command:

```bash
flask --version
```

If Flask is installed, this command will display the Flask version. If it's not installed, you'll see an error message.

**3. Install Flask:**

If Flask is not installed, you can install it using `pip`, which is the Python package manager. Open your terminal or command prompt and run the following command:

```bash
pip install Flask
```

This command will download and install Flask and its dependencies.

**4. Verify Flask Installation:**

After installing Flask, you can verify that it's installed correctly by running the `flask --version` command again. It should now display the Flask version.

**5. Test Flask:**

You can create a simple Flask application to test if it's working. Create a Python file, such as `app.py`, with the following code:

```python
from flask import Flask

app = Flask(__name)

@app.route('/')
def hello():
    return 'Hello, Flask!'

if __name__ == '__main__':
    app.run()
```

Save the file, and in your terminal or command prompt, navigate to the directory where `app.py` is located. Then run the following command:

```bash
python app.py
```

This will start a development server, and you should see output indicating that the Flask app is running. Open a web browser and go to `http://127.0.0.1:5000/`, and you should see "Hello, Flask!" displayed in your browser. This confirms that Flask is working on your desktop.
### ---------------------------------------------------------------------------------
### How to Run Python Flask Project ?
To run a Python Flask project, follow these steps:

1. **Navigate to Your Project Directory:**
   Open your terminal or command prompt and navigate to the directory where your Flask project is located. You should be in the directory containing your Flask application file (usually named `app.py`) and any associated files and folders.

2. **Activate a Virtual Environment (if used):**
   If you are using a virtual environment (recommended), activate it by running the appropriate command based on your operating system:

   - On Windows:

     ```
     venv\Scripts\activate
     ```

   - On macOS and Linux:

     ```
     source venv/bin/activate
     ```

   Activating the virtual environment isolates your project's dependencies from the system-wide Python installation.

3. **Run the Flask Application:**
   In the terminal, while inside your project directory and with the virtual environment activated (if used), run the Flask application by executing the `flask run` command. For example:

   ```
   flask run
   ```

   This command starts the Flask development server and should display output similar to the following:

   ```
    * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
   ```

   This indicates that your Flask app is running locally, and you can access it by visiting `http://127.0.0.1:5000/` in your web browser.

4. **Access Your Flask App:**
   Open a web browser and navigate to the URL `http://127.0.0.1:5000/` or `http://localhost:5000/`. You should see your Flask application running. If you have defined routes in your Flask app, you can access them by navigating to the appropriate URLs as defined in your routes.

5. **Interact with Your Flask App:**
   You can interact with your Flask app by using the web interface in your browser or by making HTTP requests programmatically using tools like `curl` or libraries like `requests` in Python.

6. **To Stop the Flask Development Server:**
   To stop the Flask development server, go back to your terminal and press `Ctrl+C`. This will halt the server, and you'll see a message like " * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)".

Your Flask application is now up and running, and you can continue to develop and test it. Be sure to make changes in your Flask code, templates, or static files, and the development server will automatically reload to reflect those changes as you save them.


### ---------------------------------------------------------------------------------
### Flask Framwork Issues
### Issue
```bash
flask --version
```
```bash
flask : The term 'flask' is not recognized as the name of a cmdlet, function, script file, or operable program. Check
the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ flask --version
+ ~~~~~
    + CategoryInfo          : ObjectNotFound: (flask:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```
### Solution
```bash
python -m flask --version
```

### Issue
```bash
venv\Scripts\activate
venv\Scripts\activate : The module 'venv' could not be loaded. For more information, run 'Import-Module venv'.
At line:1 char:1
+ venv\Scripts\activate
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (venv\Scripts\activate:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CouldNotAutoLoadModule
```
### Solution
The error message you're encountering indicates that the `venv` module couldn't be loaded, and it's likely because you're using PowerShell in Windows. The `activate` script is meant to be run in Command Prompt, not PowerShell. Here's how you can activate the virtual environment in PowerShell:

1. **Check Virtual Environment Name:**
   First, ensure you are in the correct directory where your virtual environment (e.g., `venv`) is located. You can use the `ls` command to list the contents of the directory and confirm that your virtual environment is present.

2. **Change Execution Policy (if needed):**
   By default, PowerShell may have restrictions on running scripts. You might need to change the execution policy to allow running scripts. Open PowerShell as an administrator and run the following command:

   ```powershell
   Set-ExecutionPolicy RemoteSigned
   ```

   You can choose a less restrictive execution policy if security isn't a concern.

3. **Activate the Virtual Environment:**
   In PowerShell, you can activate the virtual environment using the `Activate.ps1` script. Here's how you can do it:

   ```powershell
   .\venv\Scripts\Activate.ps1
   ```

   Make sure to use a dot (`.`) before the backslash to run the script in the current context.

After running the `Activate.ps1` script, your virtual environment should be activated. You'll see the virtual environment name in your PowerShell prompt, indicating that the virtual environment is active. You can now proceed to run your Flask project within the virtual environment.
### ---------------------------------------------------------------------------------

