Project Name: demo-one
📌 Overview

This project uses Vue 3 and Spring Boot 3 to build a simple front-end and back-end separated login authentication system.

It demonstrates a complete login workflow, including login form validation, token generation and storage, automatic token attachment with Axios, backend token validation, global HTTP 401 handling, route protection, and a safe logout process.

This project is mainly designed for learning and practice, focusing on understanding how authentication works in a real front-end and back-end separated application.

🚀 Features

Designed especially for learning front-end authentication flow

Login page built with Vue 3 Composition API and Element Plus

Form validation for username and password

Token-based login system

Token stored in localStorage

Axios request interceptor for automatic token injection

Backend token validation

Global HTTP 401 Unauthorized handling on the frontend

Route protection using Vue Router guards

Logout functionality with frontend and backend token invalidation

A good example for debugging in browser Developer Tools (Console / Network)

Clear demonstration of front-end and back-end separation

🛠️ Tech Stack
Frontend

Vue 3 (Composition API)

Element Plus (UI components)

Axios (HTTP requests)

Vue Router (route navigation & route guards)

Backend

Spring Boot 3

RESTful API

Simple in-memory token storage (for learning purpose)

📂 Project Structure
Frontend (key files)
frontend/
├─ src/
│  ├─ api/
│  │  └─ auth.js              # login & logout API
│  ├─ components/
│  │  └─ LoginForm.vue        # login form UI & validation
│  ├─ router/
│  │  └─ index.js             # route config & route guards
│  ├─ utils/
│  │  └─ request.js           # axios instance & interceptors

Backend (key packages)
backend/src/main/java/com.demotest/
├─ auth/
│  └─ TokenStore.java         # in-memory token storage
├─ config/
│  └─ CorsConfig.java         # CORS configuration
├─ controller/
│  ├─ LoginController.java    # login API
│  ├─ LogoutController.java   # logout API
│  └─ ProfileController.java  # protected API
├─ dto/
│  └─ LoginRequest.java       # login request DTO
└─ DemotestApplication.java   # Spring Boot entry

📖 What I Learned

How a token-based authentication system works in a front-end and back-end separated project

The difference between route guards and Axios interceptors

How to use HTTP status codes (401) correctly instead of only business codes

How to automatically attach tokens using Axios interceptors

How to handle login expiration on the frontend in a unified way

How to debug authentication issues using Browser Developer Tools

How to design a clean and understandable project structure

🐞 Problems & Solutions
Problem 1: Frontend did not react when token was invalid

Cause: Backend returned 200 OK with { code: 401 } instead of real HTTP 401
Solution: Changed backend to return HTTP 401 Unauthorized using ResponseEntity

Problem 2: Axios interceptor did not trigger when using fetch

Cause: Axios interceptors only work for Axios requests
Solution: Used Axios (request.js) instead of fetch for testing authentication flow

Problem 3: Circular dependency error in router

Cause: Router directly imported components while Axios imported router
Solution: Used lazy loading for route components

Problem 4: Logout API returned 404

Cause: Backend was not restarted after adding new controller
Solution: Restarted Spring Boot application

🔒 Security Considerations

Token is stored in localStorage (for learning purpose)

Protected routes are guarded by Vue Router

Backend validates token on every protected request

Frontend handles token expiration globally using Axios interceptors

Logout removes token on both frontend and backend

⚠️ This project is for learning purposes and does not represent a production-level security solution.

🧩 Future Enhancements

Replace in-memory token storage with JWT

Add token expiration handling

Introduce role-based authorization

Improve UI with layout and navigation menu

Add refresh token mechanism

Use Redis for token storage

🏁 How to Run This Project
Frontend
npm create vite@latest
npm install vue-router@4
npm install element-plus --save
npm run dev

Backend
mvn spring-boot:run

**Personal insights(Chinese)**

在 Element Plus 中，el-form 作为表单的统一管理容器，负责集中管理表单的数据模型和校验规则。

在 el-form 上可以定义（以下三个）：

ref：用于获取表单组件实例，从而调用如 validate 等校验方法
:model：绑定整个表单的数据模型（通常是一个 reactive 对象）
:rules：定义字段级别的校验规则

el-form-item 作为单个表单项，负责描述具体字段的校验单元。
通过 prop 属性，将当前表单项与 model 中的某个字段进行关联，用于校验定位。

在 el-form-item 内部，el-input 等输入组件通过 v-model 与 model 中对应的字段进行双向绑定。当用户输入时，数据会直接同步更新到响应式对象中。

提交表单时，通过按钮的 @click 事件触发提交函数（如 handleLogin），在该函数中调用 el-form 实例的 validate 方法，统一根据 rules 对表单数据进行校验。
校验通过后，即可直接使用响应式数据对象中的值（如 username、password）向后端发起请求。

<script setup> 作为逻辑层，主要用于声明响应式状态、获取组件实例、编写事件处理函数和业务逻辑，从而与模板层形成清晰的职责分离。

🙋‍♂️ Author

Tao-outstanding
