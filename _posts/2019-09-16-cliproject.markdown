---
layout: post
title:      "CLIproject"
date:       2019-09-16 16:13:29 +0000
permalink:  cliproject
---


##### The first project was using Ruby programming language. At first, it was an opportunity to build a CLI file structure using Bundle gems.

* Programming language: Ruby
* Demo Menu: Visual Studio Code
* Jam: Bundler (2.0), Rake (10.0), rspec (3.0), Noko Giri (1.10.4), pry(0.12.2)
* Program Name: US Largest Companies
* Program description: This is the 10th largest US company in terms of total revenue for the fiscal year, based on The Fortune 500, an annual list edited and published by Fortune magazine.
First step - Fiscal year: Enter what you want to see in one year increments
Second step - Top 10 Companies: Enter What You Want to See Company Details
Third step - Company Information
 
Problems
1. After creating the project file structure using bundle jam, I set the nokigiri and pry jam in the spec/Gemfile. The jam setup process seemed to install correctly, and no errors occurred. However, when I wrote and executed the Nokogiri::HTML(open(...)) code, the program started to get an error saying that the wrong undefined method was found.
I searched the web for the error message and found that the version of the jam I installed might be a problem. However, all of the jams I installed were up to date.
So I decided to update the project.gemspec file and theses two lines were added -spec.add_dependency "nokogiri”, spec.add_dependency "pry”.
After then, the problem was solved.

2. The site I decided to scrap was Fortune 500. Scraping the year provided by this site with nokogiri worked without any problems. But scraping company rankings was not smooth. It didn't work out how I thought it was correct. The moment I turned to someone for help, someone else had the same problem and one opinion was already there. "could be that the site is using js to load the content and might not be able to scrape it" In the end, I had to scrape the ranking of the non-JS parts on the same site.

3. I wanted to print company data using an iteration of utilizing objects. However, lack of time did not solve the problem. I think it's leftover by hard coding.
