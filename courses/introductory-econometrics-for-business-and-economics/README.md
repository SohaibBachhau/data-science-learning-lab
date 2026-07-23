# Introductory Econometrics for Business and Economics

This directory contains my course-specific materials for
**Introductory Econometrics for Business and Economics**, part of the
**Minor Applied Econometrics** at Vrije Universiteit Amsterdam.

The course is taught by Quint Wiersma and Julia Schaumburg from
Econometrics and Data Science at Vrije Universiteit Amsterdam.

## Course purpose

The course introduces the mathematical and statistical foundations of
econometric analysis using observational data.

It develops the tools needed to:

- specify and interpret regression models;
- estimate unknown population parameters;
- understand the assumptions underlying ordinary least squares;
- study the sampling distributions of estimators;
- conduct hypothesis tests;
- construct confidence intervals;
- estimate and interpret multiple regression models;
- work with nonlinear regression functions;
- introduce panel-data and fixed-effects methods.

## Course outline

### Week 1: Simple linear regression with one regressor

Topics:

- the purpose of econometrics;
- cross-sectional, time-series and panel data;
- the population linear regression model;
- ordinary least squares estimation;
- derivation of the OLS estimators;
- predicted values and residuals;
- interpretation of regression coefficients;
- measures of fit;
- classical regression assumptions;
- maximum likelihood estimation.

### Week 2: Simple linear regression inference

Topics:

- least-squares assumptions;
- conditional mean independence;
- independently and identically distributed observations;
- finite-moment assumptions and outliers;
- estimators as random variables;
- unbiasedness of OLS;
- consistency of OLS;
- large-sample normality;
- the law of large numbers;
- the central limit theorem;
- Slutsky's theorem;
- the continuous mapping theorem;
- standard errors;
- hypothesis testing;
- confidence intervals;
- regressions with binary regressors.

### Week 3: Multiple regression estimation and assumptions

Topics:

- omitted variable bias;
- the population multiple regression model;
- matrix notation;
- vector and matrix differentiation;
- derivation of the OLS estimator in matrix notation;
- fitted values and residuals;
- measures of fit in multiple regression;
- adjusted R-squared;
- least-squares assumptions for multiple regression;
- perfect multicollinearity;
- imperfect multicollinearity;
- the dummy-variable trap;
- conditional expectation of the OLS estimator;
- conditional variance of the OLS estimator.

### Week 4: Multiple regression testing and restricted estimation

Topics:

- hypothesis tests for individual coefficients;
- confidence intervals for individual coefficients;
- joint hypothesis testing;
- linear restrictions;
- F-tests;
- chi-squared approximations;
- restricted and unrestricted regression models;
- restricted estimation;
- the method of Lagrange multipliers;
- the Wald test;
- the likelihood-ratio test;
- the Lagrange-multiplier test;
- regression specification;
- control variables.

### Week 5: Nonlinear regression functions

Topics:

- nonlinear regression functions;
- marginal effects;
- nonlinear least squares;
- numerical optimization;
- gradient descent;
- transformations that produce models linear in the parameters;
- polynomial regression;
- logarithmic transformations;
- linear-log models;
- log-linear models;
- log-log models;
- elasticities;
- interactions between binary variables;
- interactions between binary and continuous variables;
- interactions between continuous variables.

### Week 6: Introduction to panel data analysis

Topics:

- the structure of panel data;
- balanced and unbalanced panels;
- panel data with two time periods;
- first-difference estimation;
- entity-specific fixed effects;
- time fixed effects;
- two-way fixed effects;
- least-squares dummy-variable estimation;
- entity-demeaned estimation;
- panel-data assumptions;
- standard errors appropriate for panel data.

## Directory structure

```text
introductory-econometrics-for-business-and-economics/
├── README.md
├── slides/
├── course-notes/
├── assignments/
└── exam-preparation/
```

### `slides/`

Contains the original lecture slides stored locally.

The PDF files are excluded from version control and are not uploaded to
GitHub.

### `course-notes/`

Contains notes that follow the structure, notation and terminology of
this specific course.

These notes may include:

- lecture summaries;
- worked examples;
- mathematical derivations;
- explanations of course-specific notation;
- links to permanent knowledge notes.

### `assignments/`

Contains my own assignment work, code and supporting documentation.

Original assignment instructions, answer keys and restricted materials
should not be uploaded unless redistribution is permitted.

### `exam-preparation/`

Contains revision materials such as:

- condensed summaries;
- formula sheets;
- practice questions;
- common mistakes;
- exam-style derivations;
- topic checklists.

## Relationship with the knowledge base

Course-specific material is stored in this directory.

General concepts that remain useful beyond this course are developed in
the permanent `knowledge/` directory.

Examples include:

- expectation;
- conditional expectation;
- variance;
- covariance;
- ordinary least squares;
- maximum likelihood;
- unbiasedness;
- consistency;
- asymptotic normality;
- the law of large numbers;
- the central limit theorem;
- hypothesis testing;
- panel-data methods.

Course notes should link to the relevant permanent knowledge notes
rather than duplicate complete explanations.

## Source materials

The main source materials for this directory are the six weekly lecture
slide sets provided for the course.

The original PDF files remain stored locally and are excluded from Git.