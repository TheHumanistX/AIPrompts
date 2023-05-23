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


We have a components folder which holds the following:

* AddButton.js
  * The code for AddButton.js:
    ```javascript
    import React from 'react'
    import IconButton from '@mui/material/IconButton';
    import AddCircleIcon from '@mui/icons-material/AddCircle';
    import { useTheme } from '@mui/material/styles';

    const AddButton = ({ onClick, size = 'large', style }) => {
    const theme = useTheme();

      return (
        <IconButton
          onClick={onClick}
        >
          <AddCircleIcon 
          onClick={onClick}
          sx={{ color: 'buttonColor.main', ...style }}
          fontSize={size}
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

    const HeaderBar = ({ currentTaskListTitle, tasksCompleted, totalTasks }) => {
        const currentMonth = getMonth(new Date());
        // We don't want a period after May because it won't abbreviate may since it is already 3 letters long.
        const currentDate = currentMonth === 4 ? format(new Date(), 'MMM do, yyyy') : format(new Date(), 'MMM. do, yyyy');

        return (
            <Box display="flex" justifyContent="space-between" alignItems="center" p={2} width='680px' height='50px' padding="0px 30px" borderRadius='25px'     bgcolor='cardBackgroundColor.main' margin='20px 0'>
                <Typography variant="h6">{`List: ${currentTaskListTitle}`}</Typography>
                <Typography variant="h6">{`Tasks Completed: ${tasksCompleted} of ${totalTasks}`}</Typography>
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
    ```
* Lists.js
    * The code for Lists.js:  
    ```javascript
    import React from 'react';
    import { Box, Typography, IconButton, Card, CardContent } from '@mui/material';
    import { AddButton, TaskList } from './';

    const Lists = () => {
        const taskLists = [
            { id: 1, title: 'Errands', tasksCompleted: 3, totalTasks: 8, completed: false },
            { id: 2, title: 'Yardwork', tasksCompleted: 1, totalTasks: 5, completed: true },
            { id: 3, title: 'Home Chores', tasksCompleted: 5, totalTasks: 10, completed: false },
        ];

        console.log(taskLists);
        console.log(taskLists.length);
        console.log(taskLists[0]);
        console.log(taskLists[1]);
        console.log(taskLists[2]);
        console.log(taskLists[0].id);

        const taskListsLength = taskLists.length;

        const handleAddList = () => {
            // Handle adding a new task list
            console.log('Add a new task list');
        };

        return (
            <Box
                width="410px"
                height="1155px"
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
                console.log('After Map taskList: ', taskList)
                   return <TaskList key={taskList.id} taskList={taskList} />
                })}

                <Card variant="plain" onClick={handleAddList} sx={{ backgroundColor: 'cardBackgroundColor.main', mt: 'auto', ml: 'auto' }}>
                    <CardContent>
                        <AddButton />
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
    import { Box, Typography, IconButton, Menu, MenuItem } from '@mui/material';
    import MoreVertIcon from '@mui/icons-material/MoreVert';
    import { SmallMenu } from './';

    const Task = ({ task }) => {
        const [anchorEl, setAnchorEl] = useState(null);
        const { id, title, completed } = task;

        const backgroundColor = () => {
            if (id % 2 === 0) {
                console.log('Even', id % 2)
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
                >
                    <Typography 
                    variant="h6"
                    sx={{
                        textDecoration: completed ? "line-through" : "none",
                        color: completed ? "textColor.completed" : "textColor.primary",
                    }}
                    >{title}
                    </Typography>
                    <IconButton onClick={handleClick}>
                        <MoreVertIcon />
                    </IconButton>
                </Box>
                <SmallMenu anchorEl={anchorEl} handleClose={handleClose} />
                <Menu
                    anchorEl={anchorEl}
                    open={Boolean(anchorEl)}
                    onClose={handleClose}
                >
                    <MenuItem onClick={handleClose}>Edit</MenuItem>
                    <MenuItem onClick={handleClose}>Delete</MenuItem>
                </Menu>
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
    import EditNoteIcon from '@mui/icons-material/EditNote';
    import CheckIcon from '@mui/icons-material/Check';
    import ClearIcon from '@mui/icons-material/Clear';
    import DeleteIcon from '@mui/icons-material/Delete';

    import { DateCalendar } from '@mui/x-date-pickers/DateCalendar';
    import { format } from 'date-fns';

    const TaskDetails = ({ task, onEdit, onDelete, onConfirm }) => {
        const [editMode, setEditMode] = useState(false);
        const [title, setTitle] = useState(task.title);
        const [dueDate, setDueDate] = useState(task.dueDate);
        const [details, setDetails] = useState(task.details);
        console.log('task.created: ', task.created)
        const createdOn = format(new Date(task.created), 'MM/dd/yyyy');
        const dueOn = format(new Date(task.dueDate), 'MM/dd/yyyy');
        console.log('createdOn: ', createdOn);
        const currentDate = format(new Date(), 'MM/dd/yyyy');

        const handleEdit = () => {
            setEditMode(true);
        };

        const handleCancel = () => {
            setEditMode(false);
            setTitle(task.title);
            setDueDate(task.dueDate);
            setDetails(task.details);
        };

        const handleConfirm = () => {
            const updatedTask = {
                ...task,
                title,
                dueDate,
                details,
            };
            onConfirm(updatedTask);
            setEditMode(false);
        };

        const handleDelete = () => {
            onDelete(task.id);
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
                            Created: {createdOn}
                        </Typography>
                        {task.dueDate && (
                            <Typography variant="h6" mb={1}>
                                Due: {dueOn}
                            </Typography>
                        )}
                        </Box>
                        <Divider variant="middle" />
                        <Typography variant="h2" mb={2} mt={4} textAlign='center'>
                            {task.title}
                        </Typography>
                        <Typography variant="h5" 
                        sx={{ ml:'40px' }}
                        >Information</Typography>
                        <TextareaAutosize
                            rowsMin={15}
                            value={task.details}
                            disabled
                            style={{ width: '600px', height: '685px', borderRadius: '12px', borderColor: 'backgroundColor.default', resize: 'none', margin: 'auto', padding:    '12px' }}
                        />
                        <Card variant='plain' sx={{ mt: 'auto', ml: 'auto', backgroundColor: 'cardBackgroundColor.main' }}>
                        <IconButton onClick={handleEdit}>
                            <EditNoteIcon 
                            sx={{ color: 'buttonColor.main', width:45, height:45 }}

                             />
                        </IconButton>
                        </Card>
                    </>
                ) : (
                    <>
                        <Typography variant="subtitle1" mb={1}>
                            Created: {currentDate}
                        </Typography>
                        <hr />
                        <TextareaAutosize rowsMin={10} />
                        <TextField
                            label="Task Title"
                            value={title}
                            onChange={(e) => setTitle(e.target.value)}
                            fullWidth
                            margin="normal"
                            InputProps={{
                                endAdornment: (
                                    <InputAdornment position="end">
                                        <IconButton onClick={handleCancel} size="small">
                                            <ClearIcon />
                                        </IconButton>
                                    </InputAdornment>
                                ),
                            }}
                        />
                        <DateCalendar
                            label="Due Date"
                            onChange={(newValue) => setDueDate(newValue)}
                            renderInput={(params) => <TextField {...params} />}
                            fullWidth
                            margin="normal"
                        />
                        <TextareaAutosize
                            rowsMin={15}
                            value={details}
                            onChange={(e) => setDetails(e.target.value)}
                            style={{ width: '600px' }}
                        />
                        <Box display="flex" justifyContent="space-between" mt={2}>
                            <IconButton onClick={handleConfirm} size="small">
                                <CheckIcon />
                            </IconButton>
                            <IconButton onClick={handleDelete} size="small">
                                <DeleteIcon />
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
    import React from 'react';
    import { Box, Typography, IconButton } from '@mui/material';
    import MoreVertIcon from '@mui/icons-material/MoreVert';
    import { ProgressBar, SmallMenu } from './';

    const TaskList = ({ taskList }) => {
        const [anchorEl, setAnchorEl] = React.useState(null);
        console.log('TaskList: ', taskList)
        const { id, title, tasksCompleted, totalTasks } = taskList;
        const progress = (tasksCompleted / totalTasks) * 100;

        // Create a function that will set the background color of the Box dependent on wheter the 'id' is even or odd
            const backgroundColor = () => {
                if (id % 2 === 0) {
                    console.log('Even', id % 2)
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
                    padding='10px'
                    borderColor='cardBackgroundColor.alternate'
                    backgroundColor= {backgroundColor()}
                    height='115px'
                    width='380px'
                    borderRadius='12px'
                >
                    <Box display="flex" justifyContent="space-between" height='60%'>
                        <Typography variant="h6">{title}</Typography>
                        <IconButton onClick={handleClick}>
                            <MoreVertIcon style={{ position: "absolute", top: "60%" }} />
                        </IconButton>
                    </Box>
                    <Typography variant="body2">{`${tasksCompleted} of ${totalTasks} Tasks Complete`}</Typography>
                    <ProgressBar margin='10px 0 0 0' width='80%' progress={progress} />
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
    import { Box, Typography, IconButton, Card, CardContent } from '@mui/material';
    import { Task, AddButton } from './';

    const Tasks = ({ taskList }) => {
        const tasks = [
            { id: 1, title: 'Task 1', completed: false },
            { id: 2, title: 'Task 2', completed: true },
            { id: 3, title: 'Task 3', completed: false },
        ];
        const tasksCompleted = tasks.filter((task) => task.completed);
        console.log('tasks completed: ', tasksCompleted)
        const tasksOutstanding = tasks.filter((task) => !task.completed);
        console.log('tasks outstanding: ', tasksOutstanding)

        const handleAddTask = () => {
            // Handle adding a new task
            console.log('Add a new task');
        };

        return (
            <Box
                width="680px"
                height="1060px"
                bgcolor="cardBackgroundColor.main"
                p={2}
                // ml={2}
                display="flex"
                flexDirection="column"
                borderRadius='22px'
            >
                <Typography variant="h5" mb={2}>
                    {taskList.title} Tasks
                </Typography>
                <Typography variant="h6" mb={2}>
                Outstanding ({tasksOutstanding.length}): 
                </Typography>
                {tasks.map((task) => (
                    <Task key={task.id} task={task} />
                ))}

                <Card variant="plain" onClick={handleAddTask} sx={{ backgroundColor: 'cardBackgroundColor.main', mt: 'auto', ml: 'auto' }}>
                    <CardContent>
                        <AddButton />
                    </CardContent>
                </Card>
            </Box>
        );
    };

    export default Tasks;

    ```
* TestComponent.js (for testing components as we make them).
    * The code for TestComponent.js:  
    ```javascript
    import React from 'react'
    import { Box } from '@mui/material'
    import { format } from 'date-fns';
    import { AddButton, ProgressBar, HeaderBar, TaskList, Task, Lists, Tasks, TaskDetails } from './'
    const TestComponent = () => {
        const taskList1 = { id: 1, title: 'Errands', tasksCompleted: 3, totalTasks: 12 }
        const taskList2 = { id: 2, title: 'Yardwork', tasksCompleted: 7, totalTasks: 10 }
        const task1 = { id: 1, title: 'Go by bank', completed: false, dueDate: format(new Date('2023-06-26'), 'MM/dd/yyyy').toString(), details: 'Need to run by the bank   and make a deposit. Also need to ask about opening a new business savings account.', created: format(new Date('2023-05-23'), 'MM/dd/yyyy').toString()}
        const task2 = { id: 2, title: 'Pay electric bill', completed: true }

        const progress = (taskList1.tasksCompleted / taskList1.totalTasks) * 100
        return (
            <Box bgcolor='backgroundColor.default'>
                <AddButton />
                <ProgressBar progress={progress} />
                <HeaderBar currentTaskListTitle='Errands' tasksCompleted='7' totalTasks='9'/>
                <TaskList key={taskList1.id} taskList={taskList1} />
                <TaskList key={taskList2.id} taskList={taskList2} />
                <Task task={task1} />
                <Task task={task2} />
                <Lists />
                <Tasks taskList = {taskList1}/>
                <TaskDetails task={task1}/>
            </Box>
        )
    }

    export default TestComponent

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


Please review everything I have typed here a few times.  Ask me any questions about anything that is not clear. Don't just assume you can figure out what I meant if I wasnt clear, please ask me.  After that, let me know if you are ready to move forward from where we stopped (at the progress bar).


