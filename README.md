# StopWatch-Desktop-App
StopWatch GUI Application (with Python Tkinter package)

> Stopwatch-App Screenshot
<br>

![stopwatch-start](https://github.com/Nischal-Pradhan/StopWatch-Desktop-App/assets/68721650/ffd4d7eb-dcca-49d2-89b2-1384864dc75e)


#### Code:
```Python
import tkinter as tk

running = False

hours, minutes, seconds = 0, 0, 0


def start():
    global running
    if not running:
        update()
        running = True


def pause():
    global running
    if running:
        running = False
        stopWatchLabel.after_cancel(update_time)
        running = False


def reset():
    global running
    if running:
        stopWatchLabel.after_cancel(update_time)
        running = False

    global hours, minutes, seconds
    hours, minutes, seconds = 0, 0, 0
    stopWatchLabel.config(text='00:00:00')


def update():
    global hours, minutes, seconds
    seconds += 1
    if seconds == 60:
        minutes += 1
        seconds = 0
    if minutes == 60:
        hours += 1
        minutes = 0

    hours_string = f'{hours}' if hours > 9 else f'0{hours}'
    minutes_string = f'{minutes}' if minutes > 9 else f'0{minutes}'
    second_string = f'{seconds}' if seconds > 9 else f'0{seconds}'

    stopWatchLabel.config(text=hours_string + ':' +
                          minutes_string + ':' + second_string)
    global update_time
    update_time = stopWatchLabel.after(1000, update)


root = tk.Tk()
root.geometry('485x220')
root.title('StopWatch')
root.resizable(False, False)

stopWatchLabel = tk.Label(text='00:00:00', font=('Courier', 75))
stopWatchLabel.pack()

startButton = tk.Button(text='Start', height=5, width=7,
                        font=('Courier', 20), command=start)
startButton.pack(side=tk.LEFT)

pauseButton = tk.Button(text='Pause', height=5, width=7,
                        font=('Courier', 20), command=pause)
pauseButton.pack(side=tk.LEFT)

resetButton = tk.Button(text='Reset', height=5, width=7,
                        font=('Courier', 20), command=reset)
resetButton.pack(side=tk.LEFT)

exitButton = tk.Button(text='Exit', height=5, width=7,
                       font=('Courier', 20), command=root.quit)
exitButton.pack(side=tk.LEFT)

root.mainloop()
```
