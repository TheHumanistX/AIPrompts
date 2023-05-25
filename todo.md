Ok, I have a more difficult project I am starting. The project will be a webapp todo-list coded in React.

I am basing the measurements below on a 1900px width by 1200px height area. The entire app will be about 23px away from the top and bottom edges of the workspace and 34px away from the left and right edges of the workspace.

Here I will list out what piece or components the todo-list will be comprised of:

-On the left side of the workspace, there will be a 'Lists' component which runs about 1155px height and 410px width. It is tall enough that nothing can fit above or below it. 
    - This will hold all of the various todo task lists such as 'errands', 'yardwork', 'home chores', etc.  
    - Easy of these will be represented by a small card that has a rough height of 115px and rough width of 380px.  
    - Each of these cards will contain the following information:
        - Task list name in the top left
        - Number of tasks in list in the top right
        - {number of tasks complete} of {total number of tasks} (i.e. '8 of 10 Tasks Complete') below the task list name with some vertical space between them.
        - Task list completion progress bare below that
        - On the far right, below the Number of Tasks in list in the top right, but also centered vertically, will be three vertical dots which user clicks/taps to display a small menu that gives options to Edit tasks list, Delete Task List, maybe other options but definitely those two.
    - On the bottom right on the Lists component will be a small round button with a little + in it which you click or tap to add a new task list to the component.
        - When that button is clicked, a small modal will pop up asking you to input the name of the task list (that's all we need to create a new task list, just a title)

Everything else will be to the right of that tall task lists component.


Across the very top we will have:

-  To the right of the 'task lists component', there will be a header bar that is about 1080px wide and 55px tall. It will be about 30px to the right of the 'task lists' component and aligned vertically with the top of that component.
    - This header bar will display three pieces of information. 
        - On the very left, it will display 'List: {name of current task list that is open/selected}'.
        - In the middle of the bar it will display 'Tasks Completed: {# tasks completed} of {# tasks in current task list}'. 
        - On the far right of the bar it will display 'Date: {current date in Mo. Day, Year form}'

- About 30px to the right of that header bar will be a Wallet connect button
    - It will be in the top right corner of the web-app and will say 'Connect Wallet' and then when connected it will display the first 5 digits of the wallet address, three dots, then the last 2 digits of the wallet address.
    - This piece will be about 285px wide and 55px tall, to start. I want to make this all responsive after I layout the whole app eventually. It will sit about 35px from the right of the edge of the workspace.

Below those two thin top components and to the right of the task lists component will be two larger 'cards'.

The first, which is directly to the right of the task lists component and sits about 30px away from it, will be the card that is the 'tasks' component. 

- This will be about 680px wide, 1050px height.

- When a task list is selected in the task lists component, this card will display all the tasks in that task list. (i.e. If I clicked on the 'errands' task list, this would display things like 'Pick up groceries', 'Go by the bank', 'Pay electric bill', etc.)
- Each of these tasks will be a narrow little card that simply displays the task title and another 3 vertical dots button that you can tap/click to display a small menu to let you edit task, delete task, etc.
    - These little cards are roughly 600px width by 60px height.
- At the bottom of this card will be another small round button with a + inside that, when clicked, lets you add a new task to this list.

The card to the right of this will also measure roughly 680px wide by 1050px height. It will sit about 30px to the right of the Tasks component and 35px from the right edge of the workspace.

- It will display one of two components. 

        - Display all details of the currently selected task from the tasks component to its leftt, or when you click the add task button in the tasks component to the left, this card will be where you have input fields to enter all the information you want to about that task list such as task

        OR
       
       - When you click the add task button at the bottom right of the tasks component, this card will present the user with all the input fields to add the new task. We will have task name, preferred due date for task, description of task (This last piece is a large text area where you could enter a small shopping list or just details about whichever task you are adding). When that add task button is clicked, opening this component to enter details about the task.


I have imported the following libraries (at your prior suggestion):

- Material UI
    - npm install @mui/material @mui/system @emotion/react @emotion/styled 
- React Router (Using HashRouter, because we will store on IPFS/IPNS)
    - npm install react-router-dom
- fleek-storage-js because we will be using Fleek.co to host our web-app and also we will use it to add, remove, change todo list items such as tasks and task lists.
    - npm install @fleekhq/fleek-storage-js
- date-fns
    - npm install date-fns
- useForm
    - npm install react-hook-form
- Third Web JS for the wallet connection
    - npm install @thirdweb-dev/react @thirdweb-dev/sdk ethers@^5
- RReact-dnd
    - npm install react-dnd react-dnd-html5-backend

---

We decided to layout the project with the following components (at least):

1. `App` component: The root component that serves as the entry point of your application. It contains the main layout along with state management for the entire application. It can include context providers or higher-order components for state and handle any global application logic or styles.

2. `Lists` component: This component represents the left sidebar and contains all individual task lists. It manages the creation of new task lists, selecting the current task list, and other related actions.

3. `TaskList` component: Represents an individual task list item within the left sidebar. It displays the task count, completion progress, and tasks-related actions (e.g., edit or delete a list).

4. `TaskHeader` component: Represents the header bar on top of the tasks area. It displays the current active task list name, tasks completed, and current date.

5. `WalletConnect` component: Represents the wallet connect button situated in the top right corner of the app. It manages connectivity to the user's wallet.

6. `Tasks` component: A card that displays all the tasks for the currently selected task list. It manages task interactions like selecting a task, adding a new task, and other task-related actions.

7. `Task` component: Represents an individual task within the Tasks component. It displays the task title and task-related actions (e.g., edit or delete a task).

8. `TaskDetails` component: This card displays the details of the currently selected task or presents a form to create a new task. It contains all the inputs required for adding or editing a task (e.g., task name, due date, description).

9. `AddButton`: Since you find yourself using the round plus button in multiple places (Lists and Tasks components), you can create a reusable AddButton component. This component can handle a click event to open relevant dialogs (add a new task list or add a new task).

10. `ProgressBar` component: Creating this component makes sense in this case, as you want to display it in two different places - within each `TaskList` card and at the bottom of the `Tasks` component. By creating a separate `ProgressBar` component, you can maintain consistent styling and behavior across both instances, which can improve code maintainability and help adhere to the DRY (Don't Repeat Yourself) principle.

11. `SmallButton` component: The small modal menu that pops up when the vertical three dot button on a single task or tasklist is clicked. When it is called it displays "Edit", "Delete"

—

We have created the react app already as well as the App.js. 


* The App.js:

```javascript
import React, { useState } from 'react';
import { ThemeProvider } from '@mui/material/styles';
import { ThirdwebProvider } from "@thirdweb-dev/react";
import theme from './theme/theme';
import { Grid, Box, Stack } from '@mui/material';
import { Lists, Tasks, HeaderBar, WalletConnect, TaskDetails } from './components';
import todoListData from './data/todoListData';

function App() {
  // Check if task list data exists in local storage
  const taskListsJSON = localStorage.getItem('taskLists');
  // If there's no data in Local Storage, store the initial data
  if (taskListsJSON === null) {
    // Store the initial task lists in Local Storage
    localStorage.setItem('taskLists', JSON.stringify(todoListData));
  }

  // Parse the data from local storage or use the initial task lists
  const initialData = taskListsJSON !== null ? JSON.parse(taskListsJSON) : todoListData;

  // Set up state with the initial data
  const [taskLists, setTaskLists] = useState(initialData);
  const [selectedTaskList, setSelectedTaskList] = useState(null);
  const [selectedTask, setSelectedTask] = useState(null);

  const handleTaskListClick = (taskList) => {
    setSelectedTaskList(taskList);
  };

  const handleTaskClick = (task) => {
    setSelectedTask(task);
  };
  
  console.log('selectedTaskList: ', selectedTaskList)

  console.log('taskListsJSON: ', taskListsJSON);
  console.log('todoListData: ', todoListData);
  console.log('taskLists');

  return (
    <ThirdwebProvider>
    <ThemeProvider theme={theme}>
      <Box bgcolor="backgroundColor.default" style={{ padding: "23px 34px", height: "97vh" }}>
        <Grid container  gap='3vw' justifyContent='center' style={{ height: "90%" }}> 
          <Grid item container xs={3}>
            <Lists taskLists={taskLists} onTaskListClick={handleTaskListClick} />
          </Grid>
          <Grid item container xs={8}>
            <Stack width='100%' spacing={2}>
            <Box display='flex' gap='3vw'>
            <HeaderBar taskList={selectedTaskList} />
            <WalletConnect />
            </Box>
            <Box display='flex' height='100%'>
            <Tasks taskList={selectedTaskList} onTaskClick={handleTaskClick} />
            <TaskDetails task={selectedTask} />
            </Box>
            </Stack>
          </Grid>
        </Grid>
      </Box>
    </ThemeProvider>
    </ThirdwebProvider>
  );
}

export default App;

```

We have a components folder which holds the following:

* AddButton.js
  * The code for AddButton.js:
    ```javascript
    import React from 'react'
    import IconButton from '@mui/material/IconButton';
    import AddCircleIcon from '@mui/icons-material/AddCircle';

    const AddButton = ({ onClick }) => {

      return (
        <IconButton
          onClick={onClick}
        >
          <AddCircleIcon 
          sx={{ color: 'buttonColor.main' }}
          fontSize='large'
          />
        </IconButton>
      );
    };

    export default AddButton;
    ```
* HeaderBar.js
    * The code for HeaderBar.js:  
    ```javascript
    import React from 'react';
    import { Typography, Box } from '@mui/material';
    import { format, getMonth } from 'date-fns';

    const HeaderBar = ({ taskList }) => {
        const currentMonth = getMonth(new Date());
        // We don't want a period after May because it won't abbreviate may since it is already 3 letters long.
        const currentDate = currentMonth === 4 ? format(new Date(), 'MMM do, yyyy') : format(new Date(), 'MMM. do, yyyy');
        const { listId, listName, tasks } = taskList || {};
        const tasksCompleted = taskList ? tasks.filter((task) => task.completed).length : null;
        const totalTasks = taskList ? tasks.length : null;
        return (

            <Box display="flex" justifyContent="space-between" alignItems="center" p={2} width='100%' height='50px' padding="0px 30px" borderRadius='25px'      bgcolor='cardBackgroundColor.main' >

                <Typography variant="h6">{`List: ${ taskList ? listName : null}`}</Typography>
                <Typography variant="h6">{`Tasks Completed: ${taskList ? tasksCompleted : null} of ${taskList ? totalTasks : null}`}</Typography>
                <Typography variant="h6">{`Date: ${currentDate}`}</Typography>

            </Box>
        );
    };

    export default HeaderBar;
    ```
* index.js (for exporting all the components)
    * The code for index.js:  
    ```javascript
    export { default as AddButton } from './AddButton';
    export { default as TestComponent } from './TestComponent';
    export { default as ProgressBar } from './ProgressBar';
    export { default as HeaderBar } from './HeaderBar';
    export { default as TaskList } from './TaskList';
    export { default as Task } from './Task';
    export { default as SmallMenu } from './SmallMenu';
    export { default as Lists } from './Lists';
    export { default as Tasks } from './Tasks';
    export { default as TaskDetails } from './TaskDetails';
    export { default as VerticalDots } from './VerticalDots';
    export { default as WalletConnect } from './WalletConnect';
    ```
* Lists.js
    * The code for Lists.js:  
    ```javascript
    import React from 'react';
    import { Box, Typography, Card, CardContent } from '@mui/material';
    import { AddButton, TaskList } from './';

    const Lists = ({ taskLists, onTaskListClick }) => {


        const taskListsLength = taskLists.length;

        const handleAddList = () => {
            // Handle adding a new task list

        };

        return (
            <Box
                width="100%"
                height="100%"
                bgcolor="cardBackgroundColor.main"
                p={2}
                display="flex"
                flexDirection="column"
                borderRadius="22px"
            >
                <Typography variant="h5" mb={2}>
                    Lists ({taskListsLength})
                </Typography>

                {taskLists.map((taskList) => {
                    console.log('taskList.listId: ', taskList.listId)
                   return <TaskList key={taskList.listId} taskList={taskList} onTaskListClick={onTaskListClick} />
                })}

                <Card variant="plain" sx={{ backgroundColor: 'cardBackgroundColor.main', mt: 'auto', ml: 'auto' }}>
                    <CardContent>
                        <AddButton onClick={handleAddList}/>
                    </CardContent>
                </Card>
            </Box>
        );
    };

    export default Lists;

    ```
* ProgressBar.js
    * The code for ProgressBar.js:  
    ```javascript
    import React from 'react';
    import { LinearProgress } from '@mui/material';

    const ProgressBar = ({ progress, width, margin, padding }) => {

      return (
        <LinearProgress
          variant="determinate"
          value={progress}
          sx={{
            height: '10px', // Adjust height
            width: width || '50%', // Adjust width
            margin: margin || '0px', // Adjust margin
            padding: padding || '0px', // Adjust padding
            borderRadius: '25px', // Round the ends 
            border: '1px solid', // Add a border
            borderColor: 'cardBackgroundColor.alternate', // Adjust the border color   
            bgcolor: 'cardBackgroundColor.main', // Adjust the background color
            '& .MuiLinearProgress-bar': {
              bgcolor: 'backgroundColor.default', // Adjust the filled bar color
            },
          }}
        />
      );
    };

    export default ProgressBar;
    ```
* SmallMenu.js
    * The code for SmallMenu.js:  
    ```javascript
    import React from 'react'
    import { Menu, MenuItem } from '@mui/material'

    const SmallMenu = ({ anchorEl, handleClose }) => {
        return (
            <div>
                <Menu
                    anchorEl={anchorEl}
                    open={Boolean(anchorEl)}
                    onClose={handleClose}
                >
                    <MenuItem onClick={handleClose}>Edit</MenuItem>
                    <MenuItem onClick={handleClose}>Delete</MenuItem>
                </Menu>
            </div>
        )
    }

    export default SmallMenu

    ```
* Task.js
    * The code for Task.js:  
    ```javascript
    import React, { useState } from 'react';
    import { Box, Typography } from '@mui/material';
    import { SmallMenu, VerticalDots } from './';

    const Task = ({ task, onTaskClick }) => {
        const [anchorEl, setAnchorEl] = useState(null);
        const { taskId, taskName, dueDate, completed, description } = task;

        const backgroundColor = () => {
            if (taskId % 2 === 0) {
                return 'cardBackgroundColor.main';
            } else {
                return 'cardBackgroundColor.alternate';
            }
        };

        const handleClick = (event) => {
            setAnchorEl(event.currentTarget);
        };

        const handleClose = () => {
            setAnchorEl(null);
        };

        return (
            <div>
                <Box
                    display="flex"
                    alignItems='center'
                    justifyContent='space-between'
                    boxSizing='border-box'
                    padding='0 20px'
                    width='600px'
                    height='60px'
                    backgroundColor={backgroundColor()}
                    borderRadius='12px'
                    border='2px solid'
                    borderColor='cardBackgroundColor.alternate'
                    onClick = {() => onTaskClick(task)}
                >
                    <Typography
                        variant="h6"
                        sx={{
                            textDecoration: completed ? "line-through" : "none",
                            color: completed ? "textColor.completed" : "textColor.primary",
                        }}
                    >{taskName}
                    </Typography>

                    <VerticalDots id={taskId} onClick={handleClick} />

                </Box>
                <SmallMenu anchorEl={anchorEl} handleClose={handleClose} />

            </div>
        );
    }

    export default Task;

    ```
* TaskDetails.js
    * The code for TaskDetails.js: 
    ```javascript
    import React, { useState } from 'react';
    import {
        Box,
        Typography,
        IconButton,
        TextField,
        TextareaAutosize,
        InputAdornment,
        Card,
        Divider
    } from '@mui/material';
    import { Check, Clear, Delete, EditNote } from '@mui/icons-material';
    import { AdapterDateFns } from '@mui/x-date-pickers/AdapterDateFns';
    import { DatePicker, LocalizationProvider } from '@mui/x-date-pickers';
    import { format } from 'date-fns';

    const TaskDetails = ({ task, onEdit, onDelete, onConfirm }) => {
        const [editMode, setEditMode] = useState(false);
        const [taskName, setTaskName] = useState(task ? task.taskName : "");
        const [dueDateV, setDueDateV] = useState(task? new Date(task.dueDate) : "");
        const [description, setDescription] = useState(task ? task.description : "");

        if (!task) {
            return (
                <Box
                    width="680px"
                    height="1060px"
                    bgcolor="cardBackgroundColor.main"
                    p={2}
                    display="flex"
                    flexDirection="column"
                    borderRadius='22px'
                    justifyContent="center"
                    alignItems="center"
                >
                    <Typography variant="h5">
                        Please select a task to see the details.
                    </Typography>
                </Box>
            );
        }
        const createdDate = task.createdDate ? format(new Date(task.createdDate), 'MM/dd/yyyy') : "";
        const dueDate = task.dueDate ? format(new Date(task.dueDate), 'MM/dd/yyyy') : "";
        const currentDate = task ? format(new Date(), 'MM/dd/yyyy') : "";

        const handleEdit = () => {
            setEditMode(true);
        };

        const handleCancel = () => {
            setEditMode(false);
            setTaskName(task.taskName);
            setDueDateV(task.dueDate);
            setDescription(task.description);
        };

        const handleConfirm = () => {
            const updatedTask = {
                ...task,
                taskName,
                dueDate,
                description,
            };
            onConfirm(updatedTask);
            setEditMode(false);
        };

        const handleDelete = () => {
            onDelete(task.taskId);
        };
        return (
            <Box
                width="680px"
                height="1060px"
                bgcolor="cardBackgroundColor.main"
                p={2}
                display="flex"
                flexDirection="column"
                borderRadius='22px'
            >
                {!editMode ? (
                    <>
                        <Box display="flex" justifyContent="space-between" padding={5} boxSizing='border-box'>
                            <Typography variant="h6" mb={1}>
                                Created: {createdDate}
                            </Typography>
                            {dueDateV && (
                                <Typography variant="h6" mb={1}>
                                    Due: {dueDateV}
                                </Typography>
                            )}
                        </Box>
                        <Divider variant="middle" />
                        <Typography variant="h2" mb={2} mt={4} textAlign='center'>
                            {task.taskId}
                        </Typography>
                        <Typography variant="h5"
                            sx={{ ml: '40px' }}
                        >Information</Typography>
                        <TextareaAutosize
                            minRows={15}
                            value={task.description}
                            disabled
                            style={{ width: '600px', height: '685px', borderRadius: '12px', borderColor: 'backgroundColor.default', resize: 'none', margin: 'auto', padding:    '12px' }}
                        />
                        <Card variant='plain' sx={{ mt: 'auto', ml: 'auto', backgroundColor: 'cardBackgroundColor.main' }}>
                            <IconButton onClick={handleEdit}>
                                <EditNote
                                    sx={{ color: 'buttonColor.main', width: 45, height: 45 }}

                                />
                            </IconButton>
                        </Card>
                    </>
                ) : (
                    <>
                        <Typography variant="subtitle1" mb={1}>
                            Created: {currentDate}
                        </Typography>
                        <Divider variant="middle" />
                        <TextField
                            label="Task Title"
                            value={taskName}
                            onChange={(e) => setTaskName(e.target.value)}
                            fullWidth
                            margin="normal"
                            InputProps={{
                                endAdornment: (
                                    <InputAdornment position="end">
                                        <IconButton onClick={handleCancel} size="small">
                                            <Clear />
                                        </IconButton>
                                    </InputAdornment>
                                ),
                            }}
                        />
                        {task &&
                            <LocalizationProvider dateAdapter={AdapterDateFns}>
                                <DatePicker
                                    label="Due Date"
                                    value={dueDate}
                                    onChange={(newValue) => setDueDateV(newValue)}
                                    renderInput={(params) => <TextField {...params} />}
                                    fullWidth
                                    margin="normal"
                                />
                            </LocalizationProvider>
                        }
                        <TextareaAutosize
                            minRows={15}
                            value={description}
                            onChange={(e) => setDescription(e.target.value)}
                            style={{ width: '600px', height: '685px', borderRadius: '12px', borderColor: 'backgroundColor.default', resize: 'none', margin: 'auto', padding:    '12px' }}
                        />
                        <Box display="flex" justifyContent="space-between" mt={2}>
                            <IconButton onClick={handleConfirm} size="small">
                                <Check />
                            </IconButton>
                            <IconButton onClick={handleDelete} size="small">
                                <Delete />
                            </IconButton>
                        </Box>
                    </>
                )}
            </Box>
        );
    };

    export default TaskDetails;
    ```
* TaskList.js
    * The code for TaskList.js:  
    ```javascript
    import React, { useState } from 'react';
    import { Box, Typography } from '@mui/material';
    import { ProgressBar, SmallMenu, VerticalDots } from './';

    const TaskList = ({ taskList, onTaskListClick }) => {
        const [anchorEl, setAnchorEl] = useState(null);
        console.log('TaskList: ', taskList)
        const { listId, listName, tasks } = taskList;
         // Calculate totalTasks and tasksCompleted based on tasks array
        const totalTasks = tasks.length;
        const tasksCompleted = tasks.filter(task => task.completed).length;
        const progress = (tasksCompleted / totalTasks) * 100;
        console.log('listId: ', listId)

        const backgroundColor = () => {
            if (listId % 2 === 0) {
                return 'cardBackgroundColor.main';
            } else {
                return 'cardBackgroundColor.alternate';
            }
        };

        const handleClick = (event) => {
            setAnchorEl(event.currentTarget);
        };

        const handleClose = () => { setAnchorEl(null); };

        return (
            <div>

                <Box
                    boxSizing='border-box'
                    border='2px solid'
                    padding='20px'
                    borderColor='cardBackgroundColor.alternate'
                    backgroundColor={backgroundColor()}
                    height='auto'
                    width='100%'
                    borderRadius='12px'
                    display='flex'
                    alignItems='center'
                    onClick={() => onTaskListClick(taskList)}
                >
                    <Box
                        display='flex'
                    flexDirection='column'
                    flexGrow={1}
                    // gap={1}
                    >
                    <Typography variant="h5" gutterBottom>{listName}</Typography>
                    <Typography variant="body2">{`${tasksCompleted} of ${totalTasks} Tasks Complete`}</Typography>
                    <ProgressBar margin='10px 0 0 0' width='80%' progress={progress} />
                </Box>
                <VerticalDots listId={listId} onClick={handleClick} 
                sx={{ ml: 'auto' }} />

            </Box>
                <SmallMenu anchorEl={anchorEl} handleClose={handleClose} />
            </div>


        );
    };

    export default TaskList;
    ```
* Tasks.js
    * The code for Tasks.js:  
    ```javascript
    import React from 'react';
    import { Box, Typography, Card, CardContent } from '@mui/material';
    import { Task, AddButton } from './';

    const Tasks = ({ taskList, onTaskClick }) => {
        if (!taskList) {
            return (
                <Box
                    width="680px"
                    height="100%"
                    bgcolor="cardBackgroundColor.main"
                    p={2}
                    // ml={2}
                    display="flex"
                    flexDirection="column"
                    alignItems="center"
                    borderRadius='22px'
                >
                    <Typography variant="h5" mb={2}>
                        Please select a task list.
                    </Typography>
                </Box>
            );
        }
    
        const tasksCompleted = taskList.tasks.filter((task) => task.completed);
        console.log('tasks completed: ', tasksCompleted)
        const tasksOutstanding = taskList.tasks.filter((task) => !task.completed);
        console.log('tasks outstanding: ', tasksOutstanding)

        const handleAddTask = () => {
            // Handle adding a new task
            console.log('Add a new task');
        };

        return (
            <Box
                width="680px"
                height="100%"
                bgcolor="cardBackgroundColor.main"
                p={2}
                // ml={2}
                display="flex"
                flexDirection="column"
                alignItems="center"
                borderRadius='22px'
            >
                <Typography variant="h5" mb={2}>
                    {taskList.listName} Tasks
                </Typography>
                <Typography variant="h6" mb={2}>
                Outstanding ({tasksOutstanding.length}): 
                </Typography>
                {taskList.tasks.map((task) => (
                    <Task key={task.taskId} task={task} onTaskClick={onTaskClick} />
                ))}

                <Card variant="plain" sx={{ backgroundColor: 'cardBackgroundColor.main', mt: 'auto', ml: 'auto' }}>
                    <CardContent>
                        <AddButton onClick={handleAddTask} />
                    </CardContent>
                </Card>
            </Box>
        );
    };

    export default Tasks;

    ```
* VerticalDots.js 
    * The code for VerticalDots.js:
    ```javascript
    import React from 'react'
    import MoreVertIcon from '@mui/icons-material/MoreVert';
    import { IconButton } from '@mui/material';

    const VerticalDots = ({ id, onClick }) => {
        const vertDotsColor = () => {
            if (id % 2 === 0) {
                console.log('Even', id % 2)
                return 'cardBackgroundColor.alternate';
            } else {
                return 'cardBackgroundColor.main';
            }
        };
        return (
            <div>
                <IconButton onClick={onClick}>
                <MoreVertIcon
                    sx={{ color: vertDotsColor(), width: 35, height: 35 }}
                />
                </IconButton>
            </div>
        )
    }

    export default VerticalDots

    ```
* WalletConnect.js
    * The code for WalletConnect.js:
    ```javascript
    import React from 'react'
    import { ConnectWallet } from "@thirdweb-dev/react";
    import { Box } from '@mui/material'

    const WalletConnect = () => {
      return (
        <Box display="flex" alignItems="center" p={2} width='285px' height='50px' padding="0px 30px" borderRadius='25px'  bgcolor='cardBackgroundColor.main'>
            <ConnectWallet />
        </Box>
      )
    }

    export default WalletConnect

    ```
In the 'theme' folder we have:

* theme.js
    * The code for theme.js:
    ```javascript
    import { createTheme } from '@mui/material/styles';

    const theme = createTheme({
      palette: {
        backgroundColor: {
          default: '#52A7CC',
        },
        textColor: {
          primary: '#000000',
          completed: 'rgb(169,169,169, 0.5)',
        },
        buttonColor: {
          main: '#A5D4DC',
        },
        cardBackgroundColor: {
          main: '#F2F4F8',
          alternate: '#D9D9D9',
        },
      },
      typography: {
        fontFamily: '"Nunito", sans-serif',
      },
    });

    export default theme;
    ```


Please review everything I have typed here a few times.  Ask me any questions about anything that is not clear. Don't just assume you can figure out what I meant if I wasn't clear, please ask me.  After that, let me know if you are ready to move forward.

