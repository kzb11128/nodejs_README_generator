# Description
This application automatically generates a standard professional READE.md using your inputs in node.js command

## User Story
```
AS A developer
I WANT a README generator
SO THAT I can quickly create a professional README for a new project
```

## Acceptance Criteria
```
GIVEN a command-line application that accepts user input
WHEN I am prompted for information about my application repository
THEN a high-quality, professional README.md is generated with the title of my project and sections entitled Description, Table of Contents, 
Installation, Usage, License, Contributing, Tests, and Questions
WHEN I enter my project title
THEN this is displayed as the title of the README
WHEN I enter a description, installation instructions, usage information, contribution guidelines, and test instructions
THEN this information is added to the sections of the README entitled Description, Installation, Usage, Contributing, and Tests
WHEN I choose a license for my application from a list of options
THEN a badge for that license is added near the top of the README and a notice is added to the section of the README entitled License that 
explains which license the application is covered under
WHEN I enter my GitHub username
THEN this is added to the section of the README entitled Questions, with a link to my GitHub profile
WHEN I enter my email address
THEN this is added to the section of the README entitled Questions, with instructions on how to reach me with additional questions
WHEN I click on the links in the Table of Contents
THEN I am taken to the corresponding section of the README
```
## Usage
Uses the following code with:
- [node.js](https://nodejs.org/en/download)
- [Inquirer package](https://www.npmjs.com/package/inquirer/v/8.2.4).

```
const inquirer = require('inquirer');
const fs = require('fs');

const generateREADME = ({title, description, installation, usage, license, contributing, tests, githubUsername, emailAddress}) => 
`![License: ${license}](https://img.shields.io/badge/License-${license}-yellow.svg)

# ${title}

## Description
${description}

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)
- [Contributing](#contributing)
- [Tests](#tests)
- [Questions](#questions)

## Installation
${installation}

## Usage
${usage}

## License
Licensed under the ${license} license

## Contributing
${contributing}

## Tests
${tests}

## Questions
GitHub: [${githubUsername}](https://github.com/${githubUsername})<br />
Email: ${emailAddress}
`;


inquirer
  .prompt([
    {
      type: 'input',
      name: 'title',
      message: 'What is the title of your project?'
    },
    {
      type: 'input',
      name: 'description',
      message: 'Please provide a description of your project.'
    },
    {
      type: 'input',
      name: 'installation',
      message: 'How to install this project?'
    },
    {
      type: 'input',
      name: 'usage',
      message: 'How to use this project?'
    },
    {
      type: 'list',
      name: 'license',
      message: 'Please select a license.',
      choices: ['MIT', 'Apache', 'GPL', 'BSD', 'None']
    },
    {  
      type: 'input',
      name: 'contributing',
      message: 'How to contribute to this project?'
    },
    {
      type: 'input',
      name: 'tests',
      message: 'How to test this project?'
    },
    {
      type: 'input',
      name: 'githubUsername',
      message: 'What is your GitHub username?'
    },
    {
      type: 'input',
      name: 'emailAddress',
      message: 'Please provide your email address.'
    },
  ])
  .then((answers) => {
    const READMEContent = generateREADME(answers);
      
    fs.writeFile('sampe_README.md', READMEContent, (err) =>
      err ? console.log(err) : console.log('Successfully created README.md!')
    );
  });
```

## Application Walkthrough Video 
Link to the [walkthrough video](https://drive.google.com/file/d/1KcpAh_c57OwXm6xsMZoHVuHZrUEdnu9J/view)
