# R_task
#name_ محمد خلف حسن محمد
#read dataset
my_data=read.csv("G3_sydney_hobart_times.csv")

str(my_data)


my_data<- as.data.frame(unclass(my_data),stringsAsFactors =  TRUE)
str(my_data)
View(my_data)


#deleting "code time lesss than 3" as it have no data
my_data<- my_data [, -which(names(my_data)== "Code.Time.less.than.3")]

# Remove any rows with missing values
my_data <- na.omit(my_data)

#removing text from numeric values
my_data$Time<- gsub(" day","",my_data$Time)
View(my_data)

library("ggplot2")

#give a look at my data
summary(my_data)
head(my_data, n = 5)

tail(my_data, n = 5)


#First to see relations between features 

#convert data to numeric data
my_data <- as.data.frame(lapply(my_data, as.numeric))

correlation_matrix <- cor(my_data)
print(correlation_matrix)


#strong relation between fleet start and fleet finish

draw1 <- ggplot(my_data)
draw1 <- ggplot(my_data, aes(x=fleet_start, y=fleet_finish))
draw1 + geom_point()
#the relation is about to be linear 

#raltion between Time and year
draw_sc <- ggplot(my_data, aes(Year, Time))
draw_sc + geom_point(aes(color=fleet_finish)) + labs(x="Year", y="fleet_finished")
draw_sc + geom_point(aes(color=fleet_finish)) + stat_smooth(se=FALSE)

#tere is strong negative relation 
#years ago yeacht take long time in race, but nowadays it becomes faster and time get reduced


draw_bar <- ggplot(my_data, aes(x= fleet_finish, fill =fleet_start))
draw_bar + geom_bar()
draw_bar + geom_bar() + theme_light()
draw_bar + geom_bar() + labs(y="count")



ggplot(data = my_data, aes(x = Time, y =fleet_finish)) +geom_bar(stat = "identity")
