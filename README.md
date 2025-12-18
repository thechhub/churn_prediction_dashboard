Flask Churn Analytics Dashboard

This is a simple Flask web application that calculates and displays customer churn analytics. It pulls precomputed metrics from a data layer and renders them in a web dashboard using a Jinja2 template.

What This App Does

Loads churn-related data using a helper function (calc_data)

Calculates:

Average churn probability

High-risk customers

Churn rate by state

High-risk customers by state

Displays the results on a web page (index.html)

Project Structure
.
├── app.py               # Main Flask application
├── data.py              # Data processing logic (contains calc_data)
├── templates/
│   └── index.html       # Frontend template
└── README.md

Requirements

Python 3.8+

Flask

Pandas (very likely, since .to_dict() is used on DataFrames)

Install dependencies:

pip install flask pandas

How It Works

The root route (/) calls calc_data() from data.py

calc_data() must return four values in this exact order:

avg_churn_prob – numeric

high_risk_customers – iterable (list / DataFrame / count)

churn_rate_by_state – Pandas DataFrame

high_risk_by_state – Pandas DataFrame

DataFrames are converted to dictionaries so they can be safely rendered in Jinja templates.

Running the App

From the project root:

python app.py


Then open your browser and go to:

http://127.0.0.1:5000/

Development Notes

Debug mode is enabled by default (debug=True)

Do not use debug mode in production

Make sure index.html correctly loops over the passed dictionaries

Example Template Variables

Available in index.html:

avg_churn_prob

high_risk_customers

churn_rate_by_state (list of dicts)

high_risk_by_state (list of dicts)

Common Pitfalls

If the app crashes on startup, calc_data() is probably returning the wrong number of values

If the page loads but shows nothing, check your Jinja loops and keys

If you see serialization errors, your DataFrames aren’t clean (NaNs, non-serializable objects)

License

Use it, modify it, break it, fix it. No guarantees.
