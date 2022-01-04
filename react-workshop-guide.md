## React Workshop - Spring 2020

##### What is React?
- A JavaScript library for building user interfaces
- Framework for developing UI components

##### Why use React?
- Useful for developing complex, single-page-applications (SPAs)
- Moving away from directly manipulating HTML/DOM nodes with event listeners, etc.
- Component and data driven development

##### Prerequisites

- [Install node.js](https://nodejs.org/en/)
- Text editor with support for JSX (VS Code, Sublime with Babel plugin)

##### Goals

- Learn the basics of handling data, writing functions, and working with 3rd party libraries

---

##### Create React App
Open a terminal, `cd` into your working directory, and run:

	npx create-react-app react-workshop-app
	cd react-workshop-app
	npm i rebass
	npm i @rebass/preset emotion-theming
	npm i @rebass/forms
	npm start

In your editor, open your project directory, then navigate to the `src` directory :

	File > Open > ...react-workshop-app > open


##### 1. App.js 
~~~~
import React from 'react';

function App() {
  return (
    <div className="App">
      <h1>
         Hello!
      </h1>
    </div>
  );
}

export default App;

~~~~


##### Process
- Simplify your idea
- Prototype, iterate, and fail quickly
- The process is the idea


##### 2. App.js 
~~~~
import React from "react";
import { ThemeProvider } from "emotion-theming";
import theme from "@rebass/preset";

function App() {
  return (
    <ThemeProvider theme={theme}>
      <div className="App">
        <h1>Hello!</h1>

        <ul>
          <li> Ann </li>
          <li> Joe </li>
        </ul>
      </div>
    </ThemeProvider>
  );
}

export default App;
~~~~


##### 3. UserCard.js 
- Save `UserCard.js` in `/src`

~~~~
import React from "react";

function UserCard() {
  return (
    <div>
      <h1>User Card</h1>
    </div>
  );
}

export default UserCard;
~~~~

##### 4. App.js 
- Import the libraries from Rebass `ThemeProvider and  `theme` per the [documentation](https://rebassjs.org/getting-started/)
- Import & render `UserCard.js`

~~~~
import React from 'react';
import { ThemeProvider } from 'emotion-theming'
import theme from '@rebass/preset'
import UserCard from './UserCard'

function App() {
  return (
    <ThemeProvider theme={theme}>
      <div className="App">
        <UserCard />    
      </div>
  </ThemeProvider>
  );
}

export default App;
~~~~

##### 5. UserCard.js

- Import and add  `Box`, `Card`, `Image`,`Heading`  and  `Text` components to `UserCard.js`
- Pass the image source url to `Image`: https://tinyurl.com/yb5lhj6e

~~~~
import React from "react";
import { Box, Card, Image, Heading, Text } from "rebass";

function UserCard() {
  return (
    <Box width={256}>
      <Card>
        <Image src="https://tinyurl.com/yb5lhj6e" />
        <Box px={2}>
          <Heading as="h3">Earth!</Heading>
          <Text fontSize={0}>Lorem Ipsum</Text>
        </Box>
      </Card>
    </Box>
  );
}

export default UserCard;
~~~~


##### 6. App.js 
- Declare a new variable (`heading`) in the `App` component and pass it as a prop to `UserCard.js`

~~~~
import React from "react";
import { ThemeProvider } from "emotion-theming";
import theme from "@rebass/preset";
import UserCard from "./UserCard";

function App() {
  const heading= "New heading!";
  return (
    <ThemeProvider theme={theme}>
      <div className="App">
        <UserCard heading = {heading} />
      </div>
    </ThemeProvider>
  );
}

export default App;
~~~~

##### 7.  UserCard.js

- Replace the heading text with our new `heading` prop
- Access props (properties) via the `props.[name]` syntax 

~~~~
import React from "react";
import { Box, Card, Image, Heading, Text } from "rebass";

function UserCard(props) {
  const heading = props.heading;
  return (
    <Box width={256}>
      <Card>
        <Image src="https://tinyurl.com/yb5lhj6e" />
        <Box px={2}>
          <Heading as="h3">{heading}</Heading>
          <Text fontSize={0}>Lorem Ipsum</Text>
        </Box>
      </Card>
    </Box>
  );
}

export default UserCard;

~~~~

##### 8. App.js

- Import the `useState` hook, and declare a state variable
- `useState` returns two values, the state variable and a function to update the state
- Add a `Button` and pass to it an `onClick` handler
- Add a `<p>` element that keeps track of the count
- Render the `Button` and count below the `UserCard`

~~~~
import React, {useState} from "react";
import { ThemeProvider } from 'emotion-theming'
import theme from '@rebass/preset'
import UserCard from './UserCard'

function App() {
	const heading = "New heading!"
	const [count, setCount] = useState(0);
	
  return (
    <ThemeProvider theme={theme}>
      <div className="App">  
        <UserCard heading = {heading}/> 
        <button onClick={() => setCount(count + 1)}>
    			Update Count
  			</button>
        <p>You clicked {count} times</p>
      </div>
  </ThemeProvider>
  );
}

export default App;
~~~~

##### 9. App.js

- [Create a two column layout](https://rebassjs.org/recipes/flexbox-grid)
- Import and add `Input`, `Button`, `Flex`, `Box`, and  `Label` components
- Declare a new state variable for the `heading` render the value in a new `<p>`

~~~~
import React, { useState } from "react";
import { ThemeProvider } from "emotion-theming";
import theme from "@rebass/preset";
import UserCard from "./UserCard";

import { Flex, Button, Box } from "rebass";
import { Label, Input } from "@rebass/forms";

function App() {
  const [count, setCount] = useState(0);
  const [heading, setHeading] = useState("New heading!");

  return (
    <ThemeProvider theme={theme}>
      <Flex mx={-2}>
        <Box width={1 / 2} px={2}>
          <Button onClick={() => setCount(count + 1)} variant="outline" mr={2}>
            Update Count
          </Button>
          <p>You clicked {count} times</p>
          <Label>New Heading</Label>
          <Input id="heading" name="heading" />
          <p>
            The card heading is: <strong>{heading}</strong>
          </p>
        </Box>

        <Box width={1 / 2} px={2}>
          <UserCard heading={heading} />
        </Box>
      </Flex>
    </ThemeProvider>
  );
}

export default App;

~~~~

##### 10. App.js

- Write a function (`handleChange`) to capture the values going into the `Input` element
- `handleChange` will also update the `heading` state variable by calling `setHeading`

~~~~
import React, { useState } from "react";
import { ThemeProvider } from "emotion-theming";
import theme from "@rebass/preset";
import UserCard from "./UserCard";

import { Flex, Button, Box } from "rebass";
import { Label, Input } from "@rebass/forms";

function App() {
  const [count, setCount] = useState(0);
  const [heading, setHeading] = useState("New heading!");
  const handleChange = (event) => setHeading(event.target.value);

  return (
    <ThemeProvider theme={theme}>
      <Flex mx={-2}>
        <Box width={1 / 2} px={2}>
          <Button onClick={() => setCount(count + 1)} variant="outline" mr={2}>
            Update Count
          </Button>
          <p>You clicked {count} times</p>
          <Label>New Heading</Label>
          <Input
            onChange={(event) => handleChange(event)}
            id="heading"
            name="heading"
          />
          <p>
            The card heading is: <strong>{heading}</strong>
          </p>
        </Box>

        <Box width={1 / 2} px={2}>
          <UserCard heading={heading} />
        </Box>
      </Flex>
    </ThemeProvider>
  );
}

export default App;
        
~~~~

##### Exercise: Update the card body text using the method above

- Declare a new state variable for the body text, along with the setter function: `bodyText` & `setBodyText`
- Pass `bodyText` as a prop to `UserCard`
- Create new `Label` & `Input` components for the `bodyText`
- Write a new handler (`handleBodyTextChange`) and pass it to the new `Input` component 
- Update the `UserCard` component to reflect the changes

##### 11. App.js

~~~~
import React, { useState } from "react";
import { ThemeProvider } from "emotion-theming";
import theme from "@rebass/preset";
import UserCard from "./UserCard";
import { Flex, Button, Box } from "rebass";
import { Label, Input } from "@rebass/forms";

function App() {
  const [count, setCount] = useState(0);
  const [heading, setHeading] = useState("New heading!");
  const [bodyText, setBodyText] = useState("Initial text.");

  const handleChange = (event) => setHeading(event.target.value);
  const handleBodyTextChange = (event) => setBodyText(event.target.value);

  return (
    <ThemeProvider theme={theme}>
      <Flex mx={-2} >
        <Box width={1 / 2} px={2}>
          <Button onClick={() => setCount(count + 1)} variant="outline" mr={2}>
            Update Count
          </Button>
          <p>You clicked {count} times</p>
          <Label >New Heading</Label>
          <Input
            onChange={(event) => handleChange(event)}
            id="heading"
            name="heading"
          />

          <Label>Card Body Text</Label>
          <Input
            onChange={(event) => handleBodyTextChange(event)}
            id="bodyText"
            name="bodyText"
          />
        </Box>

        <Box width={1 / 2} px={2}>
          <UserCard heading={heading} bodyText={bodyText} />
        </Box>
      </Flex>
    </ThemeProvider>
  );
}

export default App;

        
~~~~

##### 12.  UserCard.js

- Update the `Text` component to render the `bodyText` prop 

~~~~
import React from "react";
import { Box, Card, Image, Heading, Text } from "rebass";

function UserCard(props) {
  const heading = props.heading;
  const bodyText = props.bodyText
  return (
    <Box width={256}>
      <Card>
        <Image src="https://tinyurl.com/yb5lhj6e" />
        <Box px={2}>
          <Heading as="h3">{heading}</Heading>
          <Text fontSize={0}>{bodyText}</Text>
        </Box>
      </Card>
    </Box>
  );
}

export default UserCard;

~~~~

##### 13.  data.json

- Create a new file called `data.json` under the `src/` directory

- Update the `Text` component to render the `bodyText` prop 

~~~~
[
   {
      "userId":1,
      "name":"Michelle",
      "text":"Hello - my name is Michelle.",
      "photo":"https://tinyurl.com/yb5lhj6e"
   },
   {
      "userId":2,
      "name":"Joe",
      "text":"Hi, I'm Joe.",
      "photo":"https://tinyurl.com/yd9rdwvx"
   },
   {
      "userId":3,
      "name":"Jane",
      "text":"Hello world!",
      "photo":"https://tinyurl.com/yaexgoch"
   }
]

~~~~

##### 14. App.js

- Declare new state variables: `userData` & `setData`
- Pass `userData` as a prop to `UserCard`
-  Import `Select` component and create the select options
- Declare state variable and setter for Select option: `selected` & `setSelected`
- Declare `onChange` handler for Selection: `handleSelectChange`
- Update `handleChange` & `handleBodyTextChange`

~~~~
import React, { useState } from "react";
import { ThemeProvider } from "emotion-theming";
import theme from "@rebass/preset";
import UserCard from "./UserCard";
import { Flex, Button, Box } from "rebass";
import { Label, Input, Select } from "@rebass/forms";

// New
import data from "./data.json";

function App() {
  // New
  const [userData, setData] = useState(data);
  const [selected, setSelected] = useState(1);

  const [count, setCount] = useState(0);
  const [heading, setHeading] = useState("New heading!");
  const [bodyText, setBodyText] = useState("Initial text.");

  const handleChange = (event) => {
    const newHeading = event.target.value;
    const newUserData = [...userData];
    newUserData.find((user) => user.userId == selected).name = newHeading;
    setData(newUserData);
  };
  const handleBodyTextChange = (event) => setBodyText(event.target.value);

  const handleSelectChange = (event) => {
    const selection = event.target.value;
    setSelected(selection);
  };

  return (
    <ThemeProvider theme={theme}>
      <Flex mx={-2}>
        <Box width={1 / 2} px={2}>
          <Button onClick={() => setCount(count + 1)} variant="outline" mr={2}>
            Update Count
          </Button>
          <p>You clicked {count} times</p>

          <Label>Select a User</Label>
          <Select
            id="user"
            name="user"
            defaultValue={selected}
            onChange={(event) => handleSelectChange(event)}
          >
            <option value={1}>Michelle</option>
            <option value={2}>Joe</option>
            <option value={3}>Lee</option>
          </Select>

          <Label>New Heading</Label>
          <Input
            onChange={(event) => handleChange(event)}
            id="heading"
            name="heading"
          />

          <Label>Card Body Text</Label>
          <Input
            onChange={(event) => handleBodyTextChange(event)}
            id="bodyText"
            name="bodyText"
          />
        </Box>

        <Box width={1 / 2} px={2}>
          <UserCard heading={heading} bodyText={bodyText} userData={userData} />
        </Box>
      </Flex>
    </ThemeProvider>
  );
}

export default App;
~~~~

##### 

##### 15. UserCard.js

- In UserCard, write a new component which maps through the data array and returns cards

  ~~~~
  import React from "react";
  import { Box, Card, Image, Heading, Text } from "rebass";
  
  
  const UserCards = (props) => {
    const users = props.userData;
    return users.map((user) => (
      <Box width={256}>
        <Card>
          <Image src={user.photo} />
          <Box px={2}>
            <Heading as="h3">{user.name}</Heading>
            <Text fontSize={0}>{user.text}</Text>
          </Box>
        </Card>
      </Box>
    ));
  };
  
  function UserCard(props) {
    const userData = props.userData
    return (
      <>
        <UserCards userData={userData} />
      </>
    );
  }
  
  export default UserCard;
  
  
  ~~~~