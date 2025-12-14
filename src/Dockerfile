FROM node:20-alpine AS builder
WORKDIR /build
COPY package*.json ./
RUN npm ci --only=production
COPY . .

FROM node:20-alpine AS final
RUN adduser -D -u 1000 appuser
USER appuser
WORKDIR /app
COPY --from=builder --chown=appuser:appuser /build .
EXPOSE 5000
CMD ["node", "src/index.js"]
