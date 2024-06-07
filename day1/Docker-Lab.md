# Workshop Outline: Building and Testing Docker Containers with GitHub Copilot

#### Prerequisites:
- Basic understanding of Node.js and Express framework.
- Familiarity with Docker and containerization concepts.
- Visual Studio Code installed with GitHub Copilot extension.
- Postman installed for testing APIs.

#### Step 1: Setting Up the Environment
- **Important** Check your computer to make sure you have Docker Desktop.  If not, download and install Docker Desktop for Windows from the official Docker website. Ensure you also have Node.js and npm installed by running `node -v` and `npm -v` in the terminal or command prompt.

#### Step 2: Creating a Simple Node.js and Express API
- **Important:** Start by creating a new directory for the project and initialize a new Node.js project with `npm init -y`.
- **GitHub Copilot Prompt:** "Create a simple Express server with a GET and a POST route."
- **Action:** Write the code as suggested by Copilot, explaining the purpose of each part. The GET route could return a simple message, and the POST route could echo back the received request body.

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.use(express.json());

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.post('/echo', (req, res) => {
  res.json(req.body);
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

#### Step 3: Dockerizing the Node.js Application
- **Note:** Docker can be used to containerize applications.  A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.  The Dockerfile is used to build the Docker image, which can then be run as a container. The Dockerfile for a Node.js application typically starts with a `FROM` command to specify the base image, followed by setting the working directory, copying the package.json file, installing dependencies, copying the application code, exposing the port, and defining the command to run the application.

Containers are important because they allow you to package up your application and all of its dependencies into a single image that can be run on **any machine** that has Docker installed. This makes it easy to deploy your application to different environments without having to worry about the underlying infrastructure.

- **GitHub Copilot Prompt:** "Create a Dockerfile for a Node.js application."
- **Action:** Follow the Copilot's suggestion to create a Dockerfile. Explain each command in the Dockerfile to the students.

```Dockerfile
FROM node:14

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

#### Step 4: Building and Running the Docker Container
- **Local Operation:** Demonstrate how to build the Docker image and run it as a container.
- **Commands:**
  - Build the image: `docker build -t node-app .`
  - Run the container: `docker run -p 3000:3000 node-app`
- **GitHub Copilot Prompt:** "How do I build and run a Docker container from a Dockerfile?"

#### Step 5: Testing the API with Postman
- **Instructor Note:** Show how to use Postman to send GET and POST requests to the running container.
- **Action:** Create a new request in Postman, set the URL to `http://localhost:3000/` for the GET request, and `http://localhost:3000/echo` for the POST request with a JSON body.

#### Step 6: Updating the API and Docker Image
- **Scenario:** Add a new PUT route to the API that updates a resource.
- **GitHub Copilot Prompt:** "Add a PUT route to an Express server."
- **Action:** Implement the PUT route as suggested by Copilot. Then, explain the need to rebuild the Docker image and rerun the container to reflect the changes.
- **Commands:**
  - Rebuild the image: `docker build -t node-app .`
  - Stop the running container: Find the container ID with `docker ps` and then stop it with `docker stop <container_id>`.
  - Rerun the container: `docker run -p 3000:3000 node-app`

#### Step 7: Testing the Updated API
- **Instructor Note:** Use Postman again to test the new PUT route.
- **Action:** Demonstrate creating a PUT request in Postman to the new route and discuss the expected outcome.

#### Conclusion:
- GitHub Copilot is an excellent tool for generating code snippets and Docker commands.
- Don't stop here, be sure to experiment with different API routes and Docker configurations.
