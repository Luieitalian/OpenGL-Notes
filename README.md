# OpenGL-Notes
I take OpenGL notes here.

## OpenGL
- It is just a specification. It is up to graphics card manufacturers to implement those spec.
- OpenGL is a large state machine, we just change its state and some options to render.

### GLFW
- GLFW provides us the functions to create and use OpenGL contexts & windows.

### GLAD
- We need to store function pointers to the OpenGL functions those implemented by the manufacturer in the drivers. As it is a heavy task to find those OS-specific functions, there is **GLAD** that does the job for us.

### Vertex
- It is an array of attributes per 3D coordinate. We can call it as the backbone of rendering.
- The graphics pipeline takes a vertex as input.

### Vertex Buffer Object (VBO)
- VBO is the actual collection of the data that we can refer to in code.
- We can generate the buffer object like so:
```cpp
float vertices[] = {
    -0.5f, -0.5f, 0.0f,
     0.5f, -0.5f, 0.0f,
     0.0f,  0.5f, 0.0f
};

unsigned int VBO;
glGenBuffers(1, &VBO);
```
- We first need to give it an ID so we make a uint variable called VBO, then generate `1` buffer with `glGenBuffers`.
- Then we need to bind that buffer into the GL_ARRAY_BUFFER. GL_ARRAY_BUFFER is the type for VBO.
- With `glBufferData` we can copy the data into the GL_ARRAY_BUFFER target.
```cpp
glBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
```
The fourth parameter specifies how we want the graphics card to manage the given data. This can take 3 forms:

- GL_STREAM_DRAW: the data is set only once and used by the GPU at most a few times.
- GL_STATIC_DRAW: the data is set only once and used many times.
- GL_DYNAMIC_DRAW: the data is changed a lot and used many times.
