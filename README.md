## Introduction

This assignment uses data from
the <a href="http://archive.ics.uci.edu/ml/">UC Irvine Machine
Learning Repository</a>, a popular repository for machine learning
datasets. In particular, we will be using the "Individual household
electric power consumption Data Set" which I have made available on
the course web site:


* <b>Dataset</b>: <a href="https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip">Electric power consumption</a> [20Mb]

* <b>Description</b>: Measurements of electric power consumption in
one household with a one-minute sampling rate over a period of almost
4 years. Different electrical quantities and some sub-metering values
are available.


The following descriptions of the 9 variables in the dataset are taken
from
the <a href="https://archive.ics.uci.edu/ml/datasets/Individual+household+electric+power+consumption">UCI
web site</a>:

<ol>
<li><b>Date</b>: Date in format dd/mm/yyyy </li>
<li><b>Time</b>: time in format hh:mm:ss </li>
<li><b>Global_active_power</b>: household global minute-averaged active power (in kilowatt) </li>
<li><b>Global_reactive_power</b>: household global minute-averaged reactive power (in kilowatt) </li>
<li><b>Voltage</b>: minute-averaged voltage (in volt) </li>
<li><b>Global_intensity</b>: household global minute-averaged current intensity (in ampere) </li>
<li><b>Sub_metering_1</b>: energy sub-metering No. 1 (in watt-hour of active energy). It corresponds to the kitchen, containing mainly a dishwasher, an oven and a microwave (hot plates are not electric but gas powered). </li>
<li><b>Sub_metering_2</b>: energy sub-metering No. 2 (in watt-hour of active energy). It corresponds to the laundry room, containing a washing-machine, a tumble-drier, a refrigerator and a light. </li>
<li><b>Sub_metering_3</b>: energy sub-metering No. 3 (in watt-hour of active energy). It corresponds to an electric water-heater and an air-conditioner.</li>
</ol>

## Loading the data

if(!file.exists("exdata-data-household_power_consumption.zip")) {
 temp <- tempfile()
 download.file("http://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip",temp)
 file <- unzip(temp)
 unlink(temp)
 }
 power <- read.table(file, header=T, sep=";")
 power$Date <- as.Date(power$Date, format="%d/%m/%Y")
 data <- power[(power$Date=="2007-02-01") | (power$Date=="2007-02-02"),]
 data$Global_active_power <- as.numeric(as.character(data$Global_active_power))
 data$Global_reactive_power <- as.numeric(as.character(data$Global_reactive_power))
 data$Voltage <- as.numeric(as.character(data$Voltage))
 data <- transform(data, timestamp=as.POSIXct(paste(Date, Time)), "%d/%m/%Y %H:%M:%S")
 data$Sub_metering_1 <- as.numeric(as.character(data$Sub_metering_1))
 data$Sub_metering_2 <- as.numeric(as.character(data$Sub_metering_2))
 data$Sub_metering_3 <- as.numeric(as.character(data$Sub_metering_3))


The four plots that you will need to construct are shown below. 


### Plot 1

plot1 <- function() {
        hist(data$Global_active_power, main = paste("Global Active Power"), col="red", xlab="Global Active Power (kilowatts)")
        dev.copy(png, file="plot1.png", width=480, height=480)
        dev.off()
        cat("Plot1.png has been saved in", getwd())
}
plot1()

## plot1.png has been saved in C:/Users/m.hashim/Desktop/R programming/specdata

### Plot 2

plot2 <- function() {
        plot(data$timestamp,data$Global_active_power, type="l", xlab="", ylab="Global Active Power (kilowatts)")
        dev.copy(png, file="plot2.png", width=480, height=480)
        dev.off()
        cat("plot2.png has been saved in", getwd())
}
plot2()

## plot2.png has been saved in C:/Users/m.hashim/Desktop/R programming/specdata

### Plot 3

plot3 <- function() {
        plot(data$timestamp,data$Sub_metering_1, type="l", xlab="", ylab="Energy sub metering")
        lines(data$timestamp,data$Sub_metering_2,col="red")
        lines(data$timestamp,data$Sub_metering_3,col="blue")
        legend("topright", col=c("black","red","blue"), c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  "),lty=c(1,1), lwd=c(1,1))
        dev.copy(png, file="plot3.png", width=480, height=480)
        dev.off()
        cat("plot3.png has been saved in", getwd())
}
plot3()

## plot3.png has been saved in C:/Users/m.hashim/Desktop/R programming/specdata

### Plot 4

plot4 <- function() {
        par(mfrow=c(2,2))
        
        ##PLOT 1
        plot(data$timestamp,data$Global_active_power, type="l", xlab="", ylab="Global Active Power")
        ##PLOT 2
        plot(data$timestamp,data$Voltage, type="l", xlab="datetime", ylab="Voltage")
        
        ##PLOT 3
        plot(data$timestamp,data$Sub_metering_1, type="l", xlab="", ylab="Energy sub metering")
        lines(data$timestamp,data$Sub_metering_2,col="red")
        lines(data$timestamp,data$Sub_metering_3,col="blue")
        legend("topright", col=c("black","red","blue"), c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  "),lty=c(1,1), bty="n", cex=.5) 
        
        #PLOT 4
        plot(data$timestamp,data$Global_reactive_power, type="l", xlab="datetime", ylab="Global_reactive_power")
        
        #OUTPUT
        dev.copy(png, file="plot4.png", width=480, height=480)
        dev.off()
        cat("plot4.png has been saved in", getwd())
}
plot4()

## plot4.png has been saved in C:/Users/m.hashim/Desktop/R programming/specdata
