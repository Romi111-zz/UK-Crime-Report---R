# Let's start by collecting and collating our data. 
# Our aim is to have an overview of the crimes committed at national level, namely in England, Wales and Northern Ireland.
# in a one-year period. When we downloaded the data from the data.police.uk, we received a zip folder of all the information.
#Interestingly and painfully at the same time, we discovered that, there were spreadsheets for each police force
# and for each month from January to November. That's roughly 483 spreadsheets since there was no 
# information for a police force in November. 

# First, we set the working directory for the month we need:

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Jan 17")

# We then import all the spreadsheets which have .csv extensions (all the 44 police forces)

files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)

# We now join up all the spreadsheets for all the police forces for the month.

uk_crime_jan_17 <- do.call(rbind, data_list)

#Let's check everything is correct by looking at the month column in our data set

head(uk_crime_jan_17$Month)

# Let's do the same for all the months for which we obtained data, i.e January to November 2017.

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Feb 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_feb_17 <- do.call(rbind, data_list)
head(uk_crime_feb_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Mar 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_mar_17 <- do.call(rbind, data_list)
head(uk_crime_mar_17$Month)


setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Apr 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_apr_17 <- do.call(rbind, data_list)
head(uk_crime_apr_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - May 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_may_17 <- do.call(rbind, data_list)
head(uk_crime_may_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Jun 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_jun_17 <- do.call(rbind, data_list)
head(uk_crime_jun_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Jul 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_jul_17 <- do.call(rbind, data_list)
head(uk_crime_jul_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Aug 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_aug_17 <- do.call(rbind, data_list)
head(uk_crime_aug_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Sep 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_sep_17 <- do.call(rbind, data_list)
head(uk_crime_sep_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Oct 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_oct_17 <- do.call(rbind, data_list)
head(uk_crime_oct_17$Month)

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj/UK Crimes - 17/UK Crimes - Nov 17")
files = list.files(pattern="*.csv")
data_list = lapply(files, read.csv, header = TRUE)
uk_crime_nov_17 <- do.call(rbind, data_list)
head(uk_crime_nov_17$Month)

# We now have all the spreadsheets of the police forces, all joined up according to the month.
#Now let's finalise our super dataset by combining all the months’ worth of data.

uk_crime_2017 <- do.call(rbind, list(uk_crime_jan_17, uk_crime_feb_17, uk_crime_mar_17, uk_crime_apr_17, uk_crime_may_17, uk_crime_jun_17, uk_crime_jul_17, uk_crime_aug_17, uk_crime_sep_17, uk_crime_oct_17, uk_crime_nov_17))

#That went well, we now have our super data of 483 files called uk_crime_2017
# In order not to lose our new creation when we need it, we will export the data set in a chosen directory and folder.

setwd("C:/Users/romdj/OneDrive/Doing Data Science/Intro to Data Science/INFO627.Rproj")

write.csv(uk_crime_2017, "uk_crime_2017.csv")

# To avoid any fatal errors when working on the data set in R, we will copy it to a new dataset which we will name
# crime_2017.

crime_2017 <- uk_crime_2017

# After all the preparations, it is time to process the structure of our dataset.
# The following function give us a feel of the variables, we will deal with in our dataset.

colnames(crime_2017)

# The str function gives us a snapshot of what is in our dataset, the types of data in the variables and their levels.

str(crime_2017)

# My favourite package for data exploration: funModelling. Calling funModelling will also bring the 
# other packages such as Hmisc,lattice, survival, Formula and ggplot2.

library(funModeling)

# The decribe function helps with the categorical and numerical profiling of the dataset

describe(crime_2017)

# An even more interesting way of profiling the data structure. df_status allows me to view the quantity
# and percentage of zeros and missing data for all the variables. This helps me make further decision on 
# data processing such as which column to eliminate, whether I should remove the missing data or replace them.

df_status(crime_2017)

# As mentioned above, I feel there is no point keeping the last columns since all the information is missing.

crime_2017 <- crime_2017[, -12]

# I am happy keeping all the other columns for now as you never know. I also need to investigate further the
# number of NAs for the outcome categories 2.4 of 6 million observations is still huge for such an important variable.
# Now we are ready for more discovery and summary of the data. Let's look at the frequency tables and chart 
# for our important variables. Let ‘start with the total number of crimes reported by each police force.

freq(crime_2017$Falls.within)

# How about looking at the distribution of the crimes on a map? First I need to remove the missing data from the 
# Longitude and Latitude columns. I then transform the data into spatial data points to make it easier to plot.


crime_2017_map <- na.omit(crime_2017)
crime_2017_coords <- cbind(Longitude = as.numeric(as.character(crime_2017_map$Longitude)), latitude = as.numeric(as.character(crime_2017_map$Latitude)))
library("sp")
crime_2017.pts <- SpatialPointsDataFrame(crime_2017_coords, crime_2017_map[ , -(5:6)], proj4string = CRS("+init=epsg:4326"))
plot(crime_2017.pts, pch = ".", col = "red")

# Looking at the types of crimes committed

freq(crime_2017$Crime.type)

# Looking at the number of crimes per months 

freq(crime_2017$Month)


# Number of crimes overtime
monthly <- table(crime_2017$Month)
plot(monthly, col = "purple", main = "Crimes in the UK per months", lwd = 20, type = "b", ylim = c(0, max(monthly)*1.1), ylab = "Number of crimes", xlab = "Month")

# Looking at how the offences are dealt with how the information is recorded

freq(crime_2017$Last.outcome.category)

