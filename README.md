schools
=======

#-------------------------------------------------------------------------------
# Name:        module1
# Purpose:
#
# Author:      Smith Family
#
# Created:     03/06/2014
# Copyright:   (c) Smith Family 2014
# Licence:     <your licence>
#-------------------------------------------------------------------------------
#!/usr/bin/env python


import doctest

class School:

    def __init__(self, school_name, num_pupils, num_rooms):
        """intialise instance variables"""
        self.school_name = school_name
        self.num_pupils = num_pupils
        self.num_rooms = num_rooms

    def average_pupils_per_room(self):
        return self.num_pupils/self.num_rooms

    def display_average(self):
        """
        >>> s = School("Eveyln Intermediate", 1500, 96)
        >>> s.display_average()
        Eveyln Intermediate has 15.62 pupils per room.
        """
        str_form = "{} has {:.2f} pupils per room."
        print(str_form.format(self.school_name,self.average_pupils_per_room()))


def get_info():
    global school_name
    global num_pupils
    global num_rooms
    school_name=input("What is the name of the school?")
    num_pupils=int(input("How many pupils are on the roll?"))
    num_rooms=int(input("How many classrooms are there?"))

if __name__ == '__main__':
    import doctest
    doctest.testmod(verbose = False)
    schools=[]
    num_schools=int(input("How many schools?"))
    for i in range(num_schools):
        get_info()
        schools.append(School(school_name, num_pupils, num_rooms))
    for school in schools:
        school.display_average()

    import csv
    file_name = 'schoolsdb.csv'
    ofile = open(file_name, 'w') #open with write('w') or append('a') privelages
    writer = csv.writer(ofile, delimiter=',')
    #cycles through list of records created by gui
    for i in range (0, len(schools)):
        print(schools[i])
        writer.writerow([schools[i]])
    #explicitly closes the output file
    ofile.close()
