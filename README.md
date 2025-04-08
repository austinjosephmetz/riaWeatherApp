# riaWeatherApp
Weather app sample using Vue and Tailwind for styling

to run clone the repo onto a system with NPM and within riaWeatherApp/riaWeatherAppAustinMetz/ run the following commands:

npm install
npm run dev

this will run the application on a localhost url that you can access in your browser and view the current version of the application.

Notes:
I tried my best to stay within the 2 hour (which I still kind of went outside of) window and as such was not able to fully flesh out some of the functionality which I will list here:
- Add in code for 5-day forecast. I would approach this based on using the 5-day/3-hour api. I would gather the different list items and group them based on their date. from here iterate through each date to get the high and low temps within each group and figure which weather icon to show most likely at the middle of the day and then display this info accordingly
- Add in code for search which would use a regex that would filter through the different city values we have (this likely wouldn't take long but I didn't prioritize this when working through this project)
- Update styling further to match mockup

I added the current weather card which was not in the initial problem description mostly because it was one of the the free APIs that were accessible through the api key that was given and it seemed weird not to have it. With a bit more time I would implement the grouping for the daily forecast values. I think part of the issue was just getting refreshed on working within the Vue framework as it has been some time since I have had a chance to use it.

Overall had a fun time working through this project and I appreciate the opportunity to create this project.
