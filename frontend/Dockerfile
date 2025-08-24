# Stage 1: Build React app
FROM node:18-alpine AS build

WORKDIR /app

# Copy only package.json and package-lock.json
COPY package*.json ./

# Install dependencies (npm ci is faster and reproducible)
RUN npm ci

# Copy the rest of the frontend source code
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy build output to Nginx HTML folder
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
