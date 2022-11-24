# Obsidian-Tasks-Calendar
#### A custom view build with [Obsidian-Dataview](https://github.com/blacksmithgu/obsidian-dataview) to display tasks from [Obsidian-Tasks](https://github.com/obsidian-tasks-group/obsidian-tasks) and from your daily notes in a highly customisable calendar with a wide variety of views

![Mockup](https://user-images.githubusercontent.com/59178587/203779113-753a84d1-7614-421c-b0d5-8786b2f15bc4.png)

## Story
All Obsidian and Task Plugin users love the program. What has been set up with the Task Plugin is just great and helps so many people to organize their work. However, just listing tasks according to certain criteria is sometimes a bit boring. To get a quick visual impression of one's workday/workweek/workmonth, a calendar view would be ideal. To be honest, I'm too stupid to program my own plugins for Obsidian, but I know some Javascript, so I programmed this Dataview snippet. I hope to offer many people a good addition to the Task Plugin and hope for an integration into the Task Plugin someday. But I'm sure there are better programmers out there, who can make my code, which is probably horrible for professionals, much better.

## Setup
1.  Install "Dataview Plugin" from the external plugins
2.  Create a new folder called "tasksCalendar" or any other name and paste the files "view.js" and "view.css" into it

    <img width="259" alt="Bildschirm­foto 2022-10-30 um 10 00 03" src="https://user-images.githubusercontent.com/59178587/198870629-392cb4fe-654a-421c-b8fb-d4b66def329b.png">

3.  Create a new note or edit an existing one and add the following code line:

    ````
    ```dataviewjs
    await dv.view("tasksCalendar", {pages: "", view: "month", firstDayOfWeek: 1, options: "style1"})
    ```
    ````
    
    If you paste the main files (js/css) into another folder then "tasksCalendar", you have to replace the name between the first quotation marks.
 
 4. There are 4 different variables to set path/location as "pages", calendar view style as "view", first day of the week (0 or 1) as "firstDayOfWeek" and some style classes as "options"

---
## Required parameters

### pages:

For help and instruction take a look here [Dataview Help](https://blacksmithgu.github.io/obsidian-dataview/api/code-reference/#dvpagessource)

```
pages: ""
```
Get all tasks from all notes in obsidian.

```
pages: '"Task Management/Work"'
```
Set a custom folder to get tasks from.

The dv.pages command is the same and works exactly the same like in dataview-plugin.

```
pages: "dv.pages().file.tasks.where(t => t.tags.includes('#Pierre'))"
pages: "dv.pages().file.tasks.where(t=>!t.checked && t.header.subpath != 'Log')"
```
It is also possible to define complex queries. These must start with `dv.pages` and output tasks as a result.
    

### view:
```
view: "month"
view: "week"
```
With the view parameter you can set the default selected calendar
  

### firstDayOfWeek:
```
firstDayOfWeek: 1
firstDayOfWeek: 0
```
Set monday (1) or sunday (0) as first day of week

---
## Optional parameters

### dailyNoteFolder:
```
dailyNoteFolder: "MyCustomFolder"
dailyNoteFolder: "Inbox/Daily Notes/Work"
```
This parameter must only be specified if this is to be used. Here you can define a custom folder path for the daily notes if they should not be saved in the default folder for new files. Of course, folder structures with several levels can also be defined here. This paramter 

### startPosition:
```
startPosition: "2024-06-01"
```
This parameter is optional and can be used to set a date to give focus on a custom month/week after load. On month calendar every date between the first and the last day of the month will be shown the right month. On the week calendar all dates between the first day and the last day of that week will be shown the right week. The input format must look like this `YYYY-MM-DD`.

### globalTaskFilter:
```
globalTaskFilter: "#task"
```
This parameter must only be specified if this is to be used. Set a global task filter to hide from task text/description inside tasks-calendar.

---
## Options parameter

```
options: "noIcons"
```
Hide Task plugin Icons in front of each task

```
options: "noProcess"
```
The tasks with a start- and due-date are not displayed on all days between them

```
options: "noDailyNote"
```
Hide daily notes inside calendar

```
options: "noCellNameEvent"
```
Disable pointer events for cell names to prevent unintentional execution and thus opening of a daily note.

```
options: "mini"
```
Reduces the calendar width, height and font sizes to a more compact format
On mobile devices, the font size is automatically reduced (on some views) because the limited screen size.

```
options: "noWeekNr"
```
Hide the week number in front of each week-wrapper inside the month calendar. After deactivation, it is unfortunately no longer possible to jump directly to a desired week.

```
options: "noFilename"
```
Hides the task header line with the note file name

```
options: "lineClamp1"
options: "lineClamp2"
options: "lineClamp3"
options: "noLineClamp"
```
Set a line clamp from 1-3 inside your displayed tasks. By default 1 line is set. Alternative you can disable line clamp and show full task description text.

```
options: "noLayer"
```
The back layer of the grid with the month or week information can be hidden with this.


---

### Style options

```
options: "style1"
```
There are different style options (style1, style2, ...) to change the look of the weekly calendar view. The style inside the dataviewjs code block is set as default. However, you can switch between the individual styles at any time in the calendar itself by clicking the Week View button again.

![Style_Switcher](https://user-images.githubusercontent.com/59178587/203377096-d4e03471-007a-4d9f-86c3-9274a2329f7c.png)

---

## Note color & icon
In each note file you can define custom "color" and "icon" to show up in the calendar. To do so, you only need to add the following metadata to the first line of your note. By default the note-color is used for the dimmed background and as text-color. If you would like to give your tasks a completely different color then the note-color itself, then use the textColor meta.

```
---
color: "#bf5af2"
textColor: "#000000"
icon: "❤️"
---
```
    
The color should be hex in quotation marks to work properly. This color is set for text and as semi-transparent background. The icon itself is placed in front of each task to help identify where this task comes from.

---

## Filter
On the upper left corner of each calendar-view is a filter-icon to show or hide all done and cancelled tasks. The default-filter is set by options. If you have `filter` inside your options parameter, the filter is enabled by default.

<img width="144" alt="Bildschirm­foto 2022-11-22 um 18 54 39" src="https://user-images.githubusercontent.com/59178587/203386541-fde8e574-87dc-4cb5-9271-3c791356f73e.png">


---

## Statistic and focus

On the upper right corner is statistic button which opens a detailed list of all your tasks for the currently selected month/week. By selecting a task type you can focusing this tasks and dimm out all others. This way you can find the tasks you are looking for more easily.

Through a meaningful icon and a counter, you can quickly get an overview of incompleted tasks within the selected month/week without opening the pop-up window.

<img width="171" alt="Bildschirm­foto 2022-11-22 um 18 47 24" src="https://user-images.githubusercontent.com/59178587/203385685-a2fa0d24-9bee-46e8-82a4-d342955dcb2f.png">

---

## How It Works
This snippet fetch all tasks with a date like due, start, scheduled, done. Tasks with a start and a due date are presented on all days from start to end (due). This way you can show up periods on you calendar like a holiday. This default handling can be disabled in `options` inside the dataviewjs code line by adding `noProcess`.

<img width="1115" alt="Bildschirm­foto 2022-10-30 um 10 23 43" src="https://user-images.githubusercontent.com/59178587/198871481-bd9d4b89-ff99-435c-8c30-625f27f1a4f7.png">

Hovering a task let popup a small info about the note and task (note-title: task-description). In the upper left corner is the calendar switcher, which can be used to switch between two different calendar views (month/week). Under `view` in the dataviewjs code line the default calendar view is set. When switching between the views, the calendar remains in the previous month. By clicking on the calendar header, you can return to today (the current month or week) at any time. The arrow keys in the upper right corner can be used to scroll backwards and forwards through the months/weeks. The filter in the upper right corner allows you to hide all finished tasks in the calendar. The filter itself can be switched on by default with `noDone` in the `options` within the dataviewjs code line.

<img width="1116" alt="Bildschirm­foto 2022-10-30 um 10 19 22" src="https://user-images.githubusercontent.com/59178587/198871327-7eb684f4-04ee-4155-83be-7016889b2fee.png">

After a task is completed the start- and scheduled dates are no longer needed and will be hidden. The task is now only displayed on the final completion date.
