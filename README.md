# Social Media Platform using MERN Stack

This project demonstrates the creation of a social media platform utilizing the MERN stack – MongoDB, Express, React, and Node.js. The application allows users to add posts, like posts, and comment on them.

## Table of Contents

- [Preview](#preview)
- [Prerequisites](#prerequisites)
- [Approach](#approach)
- [Steps to Create the Project](#steps-to-create-the-project)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
- [Running the Application](#running-the-application)
- [Output](#output)
- [Deployment](#deployment)
- [License](#license)

## Preview

Preview Image: Here is a preview of the final output.

![Final Project Output](https://github.com/shyamjee1645/social-media/assets/93826494/6c58cd38-133e-405a-ba93-6b1018e80a6f)
![image](https://github.com/shyamjee1645/social-media/assets/93826494/1f4414cd-de5e-455d-9766-b074b5bce4f4)


## Prerequisites

- Node.js
- MongoDB
- Express
- React
- MERN Stack knowledge

## Approach

1. The social media website was developed with a dual focus on backend using Express.js and frontend using React.
2. Express handled API routes for CRUD operations, including likes and comments, and Multer facilitated file uploads for multimedia content.
3. React was chosen for the frontend, providing an interactive user interface with components for posts, likes, and comments.
4. Axios played a pivotal role in connecting the frontend to the backend API endpoints, ensuring smooth communication.
5. The integration phase involved configuring CORS, connecting the frontend to backend API URLs, and thorough end-to-end testing for a seamless user experience.

## Steps to Create the Project

### Backend Setup

#### Step 1: Create a directory for the backend

```bash
npm init social_backend
cd social_backend
```

#### Step 2: Initialize the Express project and install dependencies

```bash
npm init -y
npm install express mongoose cors body-parser multer uuid
```

#### Folder Structure (Backend)

```
social_backend/
│
├── models/
│   └── Post.js
├── server.js
├── package.json
└── ...
```

#### models/Post.js

```javascript
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
    title: String,
    content: String,
    likes: { type: Number, default: 0 },
    comments: [{ text: String }],
});

const Post = mongoose.model('Post', postSchema);

module.exports = Post;
```

#### Step 3: Start the backend

```bash
node server.js
```

### Frontend Setup

#### Step 4: Set up React frontend

```bash
npx create-react-app social_frontend
cd social_frontend
```

#### Step 5: Install required packages

```bash
npm install axios react-router-dom
```

#### Folder Structure (Frontend)

```
social_frontend/
│
├── src/
│   ├── components/
│   │   └── CreatePost.js
│   ├── App.js
│   ├── index.js
│   ├── App.css
│   └── ...
├── package.json
└── ...
```

#### src/components/CreatePost.js

```javascript
import React, { useState } from "react";
import axios from "axios";

function CreatePost() {
    const [newPost, setNewPost] = useState({
        title: "",
        content: "",
        file: null,
    });

    const handleInputChange = (event) => {
        const { name, value } = event.target;
        setNewPost({ ...newPost, [name]: value });
    };

    const handleFileChange = (event) => {
        setNewPost({ ...newPost, file: event.target.files[0] });
    };

    const handlePostSubmit = () => {
        const formData = new FormData();
        formData.append("title", newPost.title);
        formData.append("content", newPost.content);
        formData.append("file", newPost.file);

        axios
            .post("http://localhost:5000/api/posts", formData)
            .then((response) => {
                setNewPost({ title: "", content: "", file: null });
            })
            .catch((error) => console.error("Error creating post:", error));
    };

    return (
        <div className="create-post">
            <h2>Create a Post</h2>
            <input
                type="text"
                name="title"
                placeholder="Title"
                value={newPost.title}
                onChange={handleInputChange}
            />
            <textarea
                name="content"
                placeholder="Content"
                value={newPost.content}
                onChange={handleInputChange}
            ></textarea>
            <input type="file" name="file" onChange={handleFileChange} />
            <button onClick={handlePostSubmit}>Post</button>
        </div>
    );
}

export default CreatePost;
```

#### Step 6: Start the frontend

```bash
npm start
```

## Output

Visit the deployed application at: [Social Media Platform](https://social-media-seven-sigma.vercel.app/)

## Deployment

The project is deployed on Vercel and can be accessed at the link provided above.



Feel free to customize the content as needed. Ensure the preview image URL is correct and accessible.
