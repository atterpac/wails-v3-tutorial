# V3 Tutorial
## Getting Started
### Golang Setup
- Ensure latest golang is installed
- Quick note about $GOPATH/bin
- Installing wails
- Installing task

### V3 Project Init
- Showcase end goal of tutorial
- Create new project from template of choice
- cd into project and wails3 dev
#### Breakdown of project files that are init'd 
- taskfile (in a brief sense and allude to more details later in tutorial)
- devmode.config.yaml ( more details later )
- build assets for appimage/nsis
- frontend/
- app.go and greet service
#### Example app structure that will be built
```
| main.go
| app.go
|- services
 |- system-details
  |- system-cpu.go
  |- system-process.go
  |- system-disk.go
  |- service.json
 |- models
  |- cpu.go
  |- process.go
  |- disk.go
 |- database
  |- database.go
  |- migration.go
|- frontend
  |- index.html
  ...
```

### Start example project
- Remove greet service
- Clean frontend of template 
#### Create models of what we need
- Add cpu.go with type `CPU` with fields for usage, type, name, whatever info we can pull
- Add disk.go with type `Disk` with fields for `name`, hardware `label` for drive, `Path` to the drive
- Add process.go with type `Process` with fields for `PID`, `Name`, `Uptime`, `Usage` (CPU?)
#### Create system service
- A note about services not being neccessay to function but allow to be pulled into other wails projects
- `wails3 service create` or whatever is decided
- Add system-cpu.go 
    - Pulls cpu usage and details into `models.CPU`
    - Bound function to write 
        - `GetCPU() models.CPU` 
        - `GetCPUUsage() int32`

!<--- MAYBE JUMP TO CONNECTING TO UI AFTER THE FIRST ONE AND THEN SAME SAME FOR EACH --->!

- Add system-disk.go
    - Pulls a list of disks and usage( if easy cross platform ) into `[]models.Disk`
    - Bound function to write 
        - `GetDisks() []models.Disk`
        - `GetDiskByName(name string) models.Disk`
        - `GetDiskCount() int64`

- Add system-process.go
    - Pulls running processes and stores PID,Name and a few other fields into `[]models.Process`
    - Bound functions to write 
        - `GetProcesses() []models.Process`
        - `GetProcessByName(name string) models.Process`
        - `GetProcessCount() int64`

- Add system service to the app bidnings
#### Connect frontend to bound methods
- Create a card for CPU
    - Simple card to start just displaying a number
- Create a card for disk
    - Simple card that lists the number of drives connected 
- Create a simple card for process
    - Simple card that shows the number of processes

#### Build project
- More in depth breakdown of taskfile and customizing dev mode
- Packaging 

<--- Basics Done  Next section covers the events, hooks, windows ---->

### Advancing the Project 
- Event system overview
- Tailwind Setup? Should that be in the first part and just used? would make the frontend easier to show/do but not something everyone needs or will use
- Hook CPU usage to an event for every second
- Context menu to get more details about CPU card <right click>->More Info kind of thing
- @click on disks pops out new /framless/ window with more details on the disk
    - Section on Framless windows and the `--wails-draggable` attribute
- @click on Processes pop out another window with list of the processes
    - Export button to save the current process state to file? Maybe done with a registereed event from frontend to backend to show that 

--->TODO plan the following<----
- Menus somehow in this 
- User config/sqlite? Maybe a theme config?
- 

