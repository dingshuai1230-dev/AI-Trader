FROM node:20-alpine AS builder

WORKDIR /app
COPY service/frontend/package*.json /app/
RUN npm install
COPY service/frontend /app
RUN npm run build

FROM nginx:1.27-alpine
COPY service/frontend/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
