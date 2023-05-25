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