# Use a Node 19 base image
FROM node:19-alpine

# Set the working directory to /app inside the container
WORKDIR /app

# Copy package.json and package-lock.json (if present)
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy only necessary app files
COPY . .

# Set the env to "production"
ENV NODE_ENV production

# Build the app
RUN npm run build

FROM nginx:latest
COPY --from=0 /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

# Expose the port on which the app will be running (change if necessary)
EXPOSE 5011

# Start the app with `npm run preview`
CMD ["nginx", "-g", "daemon off;"]
