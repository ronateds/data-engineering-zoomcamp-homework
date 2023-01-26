## Week 1 Homework

My week 1 [homework](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2023/week_1_docker_sql/homework.md)

## Question 1. Knowing docker tags

~ docker build --help | grep "Write the image ID to the file"
      --iidfile string          Write the image ID to the file

## Question 2. Understanding docker first run

~ docker run -it --entrypoint=bash python:3.9
root@a112498ca1dd:/# pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 58.1.0
wheel      0.38.4
