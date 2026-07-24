# n8n Codespace with Duck DNS Setup

This dev container provides a pre-configured n8n environment that can be accessed via your Duck DNS domain.

## Quick Start

### 1. Create the Codespace
- Go to your GitHub repository
- Click **Code** → **Codespaces** → **Create codespace on main**
- Wait for the container to build and initialize

### 2. Configure Duck DNS

#### Get Your Duck DNS Credentials:
1. Visit https://www.duckdns.org/
2. Sign in (or create an account)
3. Create a new subdomain or use an existing one
4. Copy your **token** (keep this secret!)

#### Update Environment Variables:
In your Codespace terminal:
```bash
nano /workspace/.env.n8n
```

Update these lines:
```
WEBHOOK_TUNNEL_URL=https://your-domain.duckdns.org/
DUCK_DNS_TOKEN=your-duckdns-token-here
```

Save the file (Ctrl+O, Enter, Ctrl+X)

### 3. Start n8n

**Option A: Using direct command**
```bash
source /workspace/.env.n8n
n8n start
```

**Option B: Using Docker Compose**
```bash
cd /workspace
docker-compose -f .devcontainer/docker-compose.yml up -d
```

### 4. Access n8n

Once running, open your browser to:
```
https://your-domain.duckdns.org
```

You should see the n8n login page.

## Environment Variables

Key variables to configure in `.env.n8n`:

```env
# n8n Server
N8N_HOST=0.0.0.0
N8N_PORT=5678
N8N_PROTOCOL=https

# Duck DNS (IMPORTANT: Update with your values)
WEBHOOK_TUNNEL_URL=https://your-domain.duckdns.org/
DUCK_DNS_TOKEN=your-token

# Database
DB_TYPE=sqlite

# Execution
EXECUTIONS_MODE=regular

# Security
SECURE_COOKIE=true
COOKIE_KEYS=your-secure-random-string
```

## Accessing from External Devices

Since you're using Duck DNS, n8n will be accessible from:
- Your local machine: https://your-domain.duckdns.org
- Other machines on your network: https://your-domain.duckdns.org
- Mobile devices: https://your-domain.duckdns.org

## Port Forwarding (if needed)

If the Codespace port isn't automatically forwarded:
1. In VS Code (Codespace), look for the **Ports** panel
2. You should see port 5678 listed
3. The green indicator means it's public
4. Click the **Open in Browser** button or copy the forwarded URL

## Stopping n8n

In your Codespace terminal:
```bash
# If running directly
Ctrl+C

# If using Docker Compose
docker-compose -f .devcontainer/docker-compose.yml down
```

## Troubleshooting

### n8n not accessible via Duck DNS
- Verify your Duck DNS domain is active at https://www.duckdns.org/
- Check the `WEBHOOK_TUNNEL_URL` matches your domain exactly
- Ensure HTTPS is being used

### Port 5678 not forwarding
- Check the Ports panel in VS Code
- Make sure the port visibility is set to "Public"
- Refresh the page if recently set

### Connection timeout
- Check if n8n process is running: `ps aux | grep n8n`
- Check the logs: `n8n start` (should show output)
- Verify firewall settings

## Data Persistence

Your n8n data is stored in:
- `/home/node/.n8n` (within the container)
- Mounted volumes persist even when the Codespace stops

## Security Notes

⚠️ **Important:**
- Never commit `.env.n8n` with real credentials to Git
- Add `.env.n8n` to `.gitignore` if it contains secrets
- Use HTTPS with Duck DNS (not HTTP)
- Change default credentials after first login
- Keep your Duck DNS token private

## Additional Resources

- [n8n Documentation](https://docs.n8n.io/)
- [Duck DNS Documentation](https://www.duckdns.org/install.jsp)
- [GitHub Codespaces Guide](https://docs.github.com/en/codespaces)

---

**Happy automating! 🚀**
