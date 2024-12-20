FROM browserless/chrome:latest

# Expose port 3000
EXPOSE 3000

# Set environment variables (defaults can be overridden by .env)
ENV ENABLE_TLS=true \
    TLS_CERT_PATH=/ssl/cert.pem \
    TLS_KEY_PATH=/ssl/key.pem

# Optionally, install any additional tools if needed
