Fabio Nelli

Python Data Analytics

With Pandas, NumPy, and Matplotlib

2nd ed.

Fabio NelliRome, Italy

Any source code or other supplementary material referenced by the author in this book is available to readers on GitHub via the book’s product page, located at www.​apress.​com/​9781484239124 . For more detailed information, please visit http://​www.​apress.​com/​source-code .

				ISBN 978-1-4842-3912-4e-ISBN 978-1-4842-3913-1

https://doi.org/10.1007/978-1-4842-3913-1

Library of Congress Control Number: 2018957991

© Fabio Nelli 2018

This work is subject to copyright. All rights are reserved by the Publisher, whether the whole or part of the material is concerned, specifically the rights of translation, reprinting, reuse of illustrations, recitation, broadcasting, reproduction on microfilms or in any other physical way, and transmission or information storage and retrieval, electronic adaptation, computer software, or by similar or dissimilar methodology now known or hereafter developed.

Trademarked names, logos, and images may appear in this book. Rather than use a trademark symbol with every occurrence of a trademarked name, logo, or image we use the names, logos, and images only in an editorial fashion and to the benefit of the trademark owner, with no intention of infringement of the trademark. The use in this publication of trade names, trademarks, service marks, and similar terms, even if they are not identified as such, is not to be taken as an expression of opinion as to whether or not they are subject to proprietary rights.

While the advice and information in this book are believed to be true and accurate at the date of publication, neither the authors nor the editors nor the publisher can accept any legal responsibility for any errors or omissions that may be made. The publisher makes no warranty, express or implied, with respect to the material contained herein.

Distributed to the book trade worldwide by Springer Science+Business Media New York, 233 Spring Street, 6th Floor, New York, NY 10013. Phone 1-800-SPRINGER, fax (201) 348-4505, e-mail orders-ny@springer-sbm.com, or visit www.springeronline.com. Apress Media, LLC is a California LLC and the sole member (owner) is Springer Science + Business Media Finance Inc (SSBM Finance Inc). SSBM Finance Inc is a Delaware corporation.

「Science leads us forward in knowledge, but only analysis makes us more aware」

This book is dedicated to all those who are constantly looking for awareness

Table of Contents

Chapter 1:​ An Introduction to Data Analysis

Data Analysis

Knowledge Domains of the Data Analyst

Computer Science

Mathematics and Statistics

Machine Learning and Artificial Intelligence

Professional Fields of Application

Understanding the Nature of the Data

When the Data Become Information

When the Information Becomes Knowledge

Types of Data

The Data Analysis Process

Problem Definition

Data Extraction

Data Preparation

Data Exploration/​Visualization

Predictive Modeling

Model Validation

Deployment

Quantitative and Qualitative Data Analysis

Open Data

Python and Data Analysis

Conclusions

Chapter 2:​ Introduction to the Python World

Python—The Programming Language

Python—The Interpreter

Python 2 and Python 3

Installing Python

Python Distributions

Using Python

Writing Python Code

IPython

PyPI—The Python Package Index

The IDEs for Python

SciPy

NumPy

Pandas

matplotlib

Conclusions

Chapter 3:​ The NumPy Library

NumPy:​ A Little History

The NumPy Installation

Ndarray:​ The Heart of the Library

Create an Array

Types of Data

The dtype Option

Intrinsic Creation of an Array

Basic Operations

Arithmetic Operators

The Matrix Product

Increment and Decrement Operators

Universal Functions (ufunc)

Aggregate Functions

Indexing, Slicing, and Iterating

Indexing

Slicing

Iterating an Array

Conditions and Boolean Arrays

Shape Manipulation

Array Manipulation

Joining Arrays

Splitting Arrays

General Concepts

Copies or Views of Objects

Vectorization

Broadcasting

Structured Arrays

Reading and Writing Array Data on Files

Loading and Saving Data in Binary Files

Reading Files with Tabular Data

Conclusions

Chapter 4:​ The pandas Library—An Introduction

pandas:​ The Python Data Analysis Library

Installation of pandas

Installation from Anaconda

Installation from PyPI

Installation on Linux

Installation from Source

A Module Repository for Windows

Testing Your pandas Installation

Getting Started with pandas

Introduction to pandas Data Structures

The Series

The DataFrame

The Index Objects

Other Functionalities on Indexes

Reindexing

Dropping

Arithmetic and Data Alignment

Operations Between Data Structures

Flexible Arithmetic Methods

Operations Between DataFrame and Series

Function Application and Mapping

Functions by Element

Functions by Row or Column

Statistics Functions

Sorting and Ranking

Correlation and Covariance

「Not a Number」Data

Assigning a NaN Value

Filtering Out NaN Values

Filling in NaN Occurrences

Hierarchical Indexing and Leveling

Reordering and Sorting Levels

Summary Statistic by Level

Conclusions

Chapter 5:​ pandas:​ Reading and Writing Data

I/​O API Tools

CSV and Textual Files

Reading Data in CSV or Text Files

Using RegExp to Parse TXT Files

Reading TXT Files Into Parts

Writing Data in CSV

Reading and Writing HTML Files

Writing Data in HTML

Reading Data from an HTML File

Reading Data from XML

Reading and Writing Data on Microsoft Excel Files

JSON Data

The Format HDF5

Pickle—Python Object Serialization

Serialize a Python Object with cPickle

Pickling with pandas

Interacting with Databases

Loading and Writing Data with SQLite3

Loading and Writing Data with PostgreSQL

Reading and Writing Data with a NoSQL Database:​ MongoDB

Conclusions

Chapter 6:​ pandas in Depth:​ Data Manipulation

Data Preparation

Merging

Concatenating

Combining

Pivoting

Removing

Data Transformation

Removing Duplicates

Mapping

Discretization and Binning

Detecting and Filtering Outliers

Permutation

Random Sampling

String Manipulation

Built-in Methods for String Manipulation

Regular Expressions

Data Aggregation

GroupBy

A Practical Example

Hierarchical Grouping

Group Iteration

Chain of Transformations

Functions on Groups

Advanced Data Aggregation

Conclusions

Chapter 7:​ Data Visualization with matplotlib

The matplotlib Library

Installation

The IPython and IPython QtConsole

The matplotlib Architecture

Backend Layer

Artist Layer

Scripting Layer (pyplot)

pylab and pyplot

pyplot

A Simple Interactive Chart

The Plotting Window

Set the Properties of the Plot

matplotlib and NumPy

Using the kwargs

Working with Multiple Figures and Axes

Adding Elements to the Chart

Adding Text

Adding a Grid

Adding a Legend

Saving Your Charts

Saving the Code

Converting Your Session to an HTML File

Saving Your Chart Directly as an Image

Handling Date Values

Chart Typology

Line Charts

Line Charts with pandas

Histograms

Bar Charts

Horizontal Bar Charts

Multiserial Bar Charts

Multiseries Bar Charts with pandas Dataframe

Multiseries Stacked Bar Charts

Stacked Bar Charts with a pandas Dataframe

Other Bar Chart Representations

Pie Charts

Pie Charts with a pandas Dataframe

Advanced Charts

Contour Plots

Polar Charts

The mplot3d Toolkit

3D Surfaces

Scatter Plots in 3D

Bar Charts in 3D

Multi-Panel Plots

Display Subplots Within Other Subplots

Grids of Subplots

Conclusions

Chapter 8:​ Machine Learning with scikit-learn

The scikit-learn Library

Machine Learning

Supervised and Unsupervised Learning

Training Set and Testing Set

Supervised Learning with scikit-learn

The Iris Flower Dataset

The PCA Decomposition

K-Nearest Neighbors Classifier

Diabetes Dataset

Linear Regression:​ The Least Square Regression

Support Vector Machines (SVMs)

Support Vector Classification (SVC)

Nonlinear SVC

Plotting Different SVM Classifiers Using the Iris Dataset

Support Vector Regression (SVR)

Conclusions

Chapter 9: Deep Learning with TensorFlow

Artificial Intelligence, Machine Learning, and Deep Learning

Artificial intelligence

Machine Learning Is a Branch of Artificial Intelligence

Deep Learning Is a Branch of Machine Learning

The Relationship Between Artificial Intelligence, Machine Learning, and Deep Learning

Deep Learning

Neural Networks and GPUs

Data Availability:​ Open Data Source, Internet of Things, and Big Data

Python

Deep Learning Python Frameworks

Artificial Neural Networks

How Artificial Neural Networks Are Structured

Single Layer Perceptron (SLP)

Multi Layer Perceptron (MLP)

Correspondence Between Artificial and Biological Neural Networks

TensorFlow

TensorFlow:​ Google’s Framework

TensorFlow:​ Data Flow Graph

Start Programming with TensorFlow

Installing TensorFlow

Programming with the IPython QtConsole

The Model and Sessions in TensorFlow

Tensors

Operation on Tensors

Single Layer Perceptron with TensorFlow

Before Starting

Data To Be Analyzed

The SLP Model Definition

Learning Phase

Test Phase and Accuracy Calculation

Multi Layer Perceptron (with One Hidden Layer) with TensorFlow

The MLP Model Definition

Learning Phase

Test Phase and Accuracy Calculation

Multi Layer Perceptron (with Two Hidden Layers) with TensorFlow

Test Phase and Accuracy Calculation

Evaluation of Experimental Data

Conclusions

Chapter 10:​ An Example— Meteorological Data

A Hypothesis to Be Tested:​ The Influence of the Proximity of the Sea

The System in the Study:​ The Adriatic Sea and the Po Valley

Finding the Data Source

Data Analysis on Jupyter Notebook

Analysis of Processed Meteorological Data

The RoseWind

Calculating the Mean Distribution of the Wind Speed

Conclusions

Chapter 11:​ Embedding the JavaScript D3 Library in the IPython Notebook

The Open Data Source for Demographics

The JavaScript D3 Library

Drawing a Clustered Bar Chart

The Choropleth Maps

The Choropleth Map of the U.​S.​ Population in 2014

Conclusions

Chapter 12:​ Recognizing Handwritten Digits

Handwriting Recognition

Recognizing Handwritten Digits with scikit-learn

The Digits Dataset

Learning and Predicting

Recognizing Handwritten Digits with TensorFlow

Learning and Predicting

Conclusions

Chapter 13:​ Textual Data Analysis with NLTK

Text Analysis Techniques

The Natural Language Toolkit (NLTK)

Import the NLTK Library and the NLTK Downloader Tool

Search for a Word with NLTK

Analyze the Frequency of Words

Selection of Words from Text

Bigrams and Collocations

Use Text on the Network

Extract the Text from the HTML Pages

Sentimental Analysis

Conclusions

Chapter 14:​ Image Analysis and Computer Vision with OpenCV

Image Analysis and Computer Vision

OpenCV and Python

OpenCV and Deep Learning

Installing OpenCV

First Approaches to Image Processing and Analysis

Before Starting

Load and Display an Image

Working with Images

Save the New Image

Elementary Operations on Images

Image Blending

Image Analysis

Edge Detection and Image Gradient Analysis

Edge Detection

The Image Gradient Theory

A Practical Example of Edge Detection with the Image Gradient Analysis

A Deep Learning Example:​ The Face Detection

Conclusions

Appendix A:​ Writing Mathematical Expressions with LaTeX

With matplotlib

With IPython Notebook in a Markdown Cell

With IPython Notebook in a Python 2 Cell

Subscripts and Superscripts

Fractions, Binomials, and Stacked Numbers

Radicals

Fonts

Accents

Appendix B:​ Open Data Sources

Political and Government Data

Health Data

Social Data

Miscellaneous and Public Data Sets

Financial Data

Climatic Data

Sports Data

Publications, Newspapers, and Books

Musical Data

Index

About the Author and About the Technical Reviewer

About the Author

Fabio Nelliis a data scientist and Python consultant, designing and developing Python applications for data analysis and visualization. He has experience with the scientific world, having performed various data analysis roles in pharmaceutical chemistry for private research companies and universities. He has been a computer consultant for many years at IBM, EDS, and Hewlett-Packard, along with several banks and insurance companies. He has an organic chemistry master’s degree and a bachelor’s degree in information technologies and automation systems, with many years of experience in life sciences (as as Tech Specialist at Beckman Coulter, Tecan, Sciex).

For further info and other examples, visit his page at https://www.meccanismocomplesso.org and the GitHub page https://github.com/meccanismocomplesso .

About the Technical Reviewer

Raul Samayoa

is a senior software developer and machine learning specialist with many years of experience in the financial industry. An MSc graduate from the Georgia Institute of Technology, he’s never met a neural network or dataset he did not like. He’s fond of evangelizing the use of DevOps tools for data science and software development.

Raul enjoys the energy of his hometown of Toronto, Canada, where he runs marathons, volunteers as a technology instructor with the University of Toronto coders, and likes to work with data in Python and R.

© Fabio Nelli 2018

Fabio NelliPython Data Analyticshttps://doi.org/10.1007/978-1-4842-3913-1_1

1. An Introduction to Data Analysis

Fabio Nelli1

(1)Rome, Italy

