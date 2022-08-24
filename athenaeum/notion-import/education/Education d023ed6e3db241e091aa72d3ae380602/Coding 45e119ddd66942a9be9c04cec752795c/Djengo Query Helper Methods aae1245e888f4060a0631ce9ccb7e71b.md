# Djengo Query Helper Methods

Last Edited: December 19, 2019 11:43 PM

Less than or Equal too:

_lte= extension on the object attribute creates less than or equal too comparison for the query

Question.objects.filter(pub_date_**_lte=**timezone.now())