# Step 1: Use an official Node.js image as a base
FROM node:18-alpine AS build

# Step 2: Set working directory
WORKDIR /app

# Step 3: Copy package files and install deps
COPY package*.json ./
RUN npm install

# Step 4: Copy all source files
COPY . .

# 🛠️ Step 5: Apply the fix here
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm run build

# Step 6: Use nginx to serve build
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
