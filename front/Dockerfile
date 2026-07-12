# syntax=docker/dockerfile:1.7
FROM node:20-alpine AS builder
WORKDIR /front
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}
COPY package*.json .
RUN npm ci
COPY . .
RUN npm run build


FROM nginx:alpine AS runtime

COPY --from=builder /front/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]