# Fuzzy Logic Simulations

A simple Python script to simulate the environment of fuzzy-logic problem in a washing machine.

## Getting Started

To get things started we will require certain python libraries in order to run this python script.

### Prerequisites
When it comes to computations NumPy is the fundamental package in terms of performing mathemetical computations and n-dimensional matrix manipulations.

First Step is to install NumPy using pip:

`pip install numpy`

This will install latest running version of NumPy in your system.

Latest version of NumPy: 1.14

scikit-fuzzy is fuzzy-logic toolkit provided by scipy. It provides a robust toolkit for performing fuzzy-logic algorithms.

Make sure if you're using NumPy then version must be >= 1.6 Otherwise scikit-fuzzy won't allow the installation. Latest stable version is avaialble on PyPi!

Again using pip we will install the latest version of scikit-fuzzy:

`pip install -U scikit-fuzzy`

If you already have scikit-fuzzy installed then this will upgrade it to a more stable version.

## Github Repo for scikit-fuzzy

`https://github.com/scikit-fuzzy/scikit-fuzzy`

## For further documentation:

`http://pythonhosted.org/scikit-fuzzy/`

# Let's dive into python code

This python script offers a simple solution to fuzzy-logic problem in a washing machine environment. There are two input variables type_of_dirtiness and degree_of_dirtiness it will represent values in percentage between 1-100 having data type as floating-point.

If we talk about output variables then there are actually two of them wash_time and amount_of_powder. Washing time will be generated according to the degree and the type of the dirtiness. In this simulation we will only generate only washing_time to make things simple enough.

Run `python main.py` a prompt will appear for you to input the parameters.

# Rule Application

Using scikit-fuzzy we will generate a Control System that will estimate how long will it take to wash one load of clothes?

Our inputs will be known as Antecednets and Outputs will be known as Consequents in a scikit-fuzzy controller.

### Antecednets(Inputs):

  - type_of_dirtiness:
     - Universe (ie, crisp value range): Determine type of dirtiness in terms of percentage 1 to 100
     - Fuzzy set (ie, fuzzy value range): NonFat, medium, Fat
     
  - degree_of_dirtiness:
     - Universe (ie, crisp value range): Determine the degree of dirtiness in terms of percentage 1 to 100
     - Fuzzy set (ie, fuzzy value range): Low,Medium,Fat

### Consequents(Outputs):

   - wash_time:
     - Universe: According to type_of_dirtiness and degree_of_dirtiness program will determine how long it would take to wash                    one load of clothes. (Output is generated in the format of minutes between (1 to 60))
     - Fuzzy set (ie, fuzzy value range): VeryShort,Short,Medium,Long,VeryLong

```python
    rule1 = ctrl.Rule(degree_dirt['High'] | type_dirt['Fat'], wash_time['VeryLong'])
    rule2 = ctrl.Rule(degree_dirt['Medium'] | type_dirt['Fat'], wash_time['long'])
    rule3 = ctrl.Rule(degree_dirt['Low'] | type_dirt['Fat'], wash_time['long'])
    rule4 = ctrl.Rule(degree_dirt['High'] | type_dirt['Medium'], wash_time['long'])
    rule5 = ctrl.Rule(degree_dirt['Medium'] | type_dirt['Medium'], wash_time['medium'])
    rule6 = ctrl.Rule(degree_dirt['Low'] | type_dirt['Medium'], wash_time['medium'])
    rule7 = ctrl.Rule(degree_dirt['High'] | type_dirt['NonFat'], wash_time['medium'])
    rule8 = ctrl.Rule(degree_dirt['Medium'] | type_dirt['NonFat'], wash_time['short'])
    rule9 = ctrl.Rule(degree_dirt['Low'] | type_dirt['NonFat'], wash_time['very_short'])
```

# Visualizing using Matplotlib

Once the output computed all together, we can visualize it,

```python
    washing_machine.washing.compute()
    washing_machine.wash_time.view(sim=washing_machine.washing)
```   

![figure_1](https://user-images.githubusercontent.com/20352413/36935274-dd39b532-1f1b-11e8-9593-995249796017.png)

Inputs that we put in were type_of_dirtiness and degree_of_dirtiness around 50 and 68 respectively, according to that washing time is generated around approximate of 32.7886891153378 minutes, we can round that up to 33 minutes.
