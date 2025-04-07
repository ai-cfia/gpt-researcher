FROM node:18.17.0-alpine as builder

ENV NEXT_PUBLIC_GPTR_API_URL=https://gptr-b.inspection.alpha.canada.ca

WORKDIR /app
COPY ./package.json ./
RUN npm install --legacy-peer-deps
COPY . .
RUN npm run build

FROM nginx

EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/out /usr/share/nginx/html
