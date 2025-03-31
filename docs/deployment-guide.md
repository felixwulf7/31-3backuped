# Deployment Guide

This guide explains how to deploy the PsyGaming Lab Website to various environments.

## Prerequisites
- Node.js 18.x or later
- npm 9.x or later
- Git

## Local Development

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/felixwulf7/28marchwebsite.git
   cd 28marchwebsite
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```
   
   The development server will start on http://localhost:3000 by default.

### Building for Production
To create a production build:
```bash
npm run build
```

This will generate optimized production files in the `.next` directory.

### Running Production Build Locally
To test the production build locally:
```bash
npm run start
```

The production server will start on http://localhost:3001 (configured in package.json).

## Deployment Options

### Option 1: Vercel Deployment (Recommended)

1. Push your code to GitHub
2. Sign up for a Vercel account: https://vercel.com
3. Import your GitHub repository
4. Select the "Next.js" framework preset
5. Configure environment variables if needed
6. Deploy

Vercel will automatically detect the Next.js project and deploy it with the best settings.

### Option 2: Traditional Web Server Deployment

1. Build the application:
   ```bash
   npm run build
   ```

2. Transfer the following files to your server:
   - `.next/` directory
   - `node_modules/` directory
   - `package.json`
   - `public/` directory
   - `next.config.js` (or `.mjs`)

3. On the server, install production dependencies:
   ```bash
   npm install --production
   ```

4. Start the production server:
   ```bash
   npm run start
   ```

5. Configure a reverse proxy (like Nginx) to forward requests to the Node.js server

### Option 3: Docker Deployment

1. Create a Dockerfile:
   ```
   FROM node:18-alpine AS base

   # Install dependencies only when needed
   FROM base AS deps
   WORKDIR /app
   COPY package.json package-lock.json ./
   RUN npm ci

   # Rebuild the source code only when needed
   FROM base AS builder
   WORKDIR /app
   COPY --from=deps /app/node_modules ./node_modules
   COPY . .
   RUN npm run build

   # Production image, copy all the files and run next
   FROM base AS runner
   WORKDIR /app
   ENV NODE_ENV production

   COPY --from=builder /app/public ./public
   COPY --from=builder /app/.next ./.next
   COPY --from=builder /app/node_modules ./node_modules
   COPY --from=builder /app/package.json ./package.json
   COPY --from=builder /app/next.config.js ./next.config.js

   EXPOSE 3001
   ENV PORT 3001

   CMD ["npm", "start"]
   ```

2. Build the Docker image:
   ```bash
   docker build -t psygaming-website .
   ```

3. Run the Docker container:
   ```bash
   docker run -p 3001:3001 psygaming-website
   ```

## Environment Variables

The following environment variables can be configured:

- `PORT`: The port the application should run on (default: 3001)
- `NODE_ENV`: The environment mode (development/production)

## Production Considerations

### Performance Optimizations
- Enable the Sharp image optimization package:
  ```bash
  npm install sharp
  ```

### Security Recommendations
- Configure Content Security Policy headers
- Set up regular security updates
- Use HTTPS in production

### Monitoring
- Consider setting up monitoring tools like:
  - New Relic
  - Datadog
  - Sentry for error tracking

### CDN Integration
For better performance, consider using a CDN for static assets:
- Cloudflare
- Akamai
- AWS CloudFront 