from flask import Flask, request, render_template_string
import requests, os

app = Flask(__name__)

CLIENT_ID = os.environ.get('CLIENT_ID')
CLIENT_SECRET = os.environ.get('CLIENT_SECRET')
DEV_TOKEN = os.environ.get('DEV_TOKEN')
CUSTOMER_ID = os.environ.get('CUSTOMER_ID')
REDIRECT_URI = 'http://localhost'

CORS = {
    'Access-Control-Allow-Origin': '*',
    'Access-Control-Allow-Headers': 'Content-Type',
    'Access-Control-Allow-Methods': 'GET, POST, OPTIONS'
}

DASHBOARD = open('dashboard.html').read() if os.path.exists('dashboard.html') else '<h1>Dashboard not found</h1>'

@app.route('/')
def home():
    return 'Sail Ads proxy running'

@app.route('/dashboard')
def dashboard():
    return render_template_string(DASHBOARD)

@app.route('/token', methods=['GET','OPTIONS'])
def get_token():
    if request.method == 'OPTIONS':
        return ('', 204, CORS)
    rt = request.args.get('refresh_token')
    code = request.args.get('code')
    payload = {'client_id':CLIENT_ID,'client_secret':CLIENT_SECRET,'grant_type':'refresh_token' if rt else 'authorization_code'}
    if rt: payload['refresh_token'] = rt
    else: payload['code'] = code; payload['redirect_uri'] = REDIRECT_URI
    r = requests.post('https://oauth2.googleapis.com/token', data=payload)
    return (r.text, r.status_code, {**CORS,'Content-Type':'application/json'})

@app.route('/campaigns', methods=['GET','OPTIONS'])
def get_campaigns():
    if request.method == 'OPTIONS':
        return ('', 204, CORS)
    token = request.args.get('access_token')
    query = "SELECT campaign.name, campaign.status, campaign_budget.amount_micros, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.conversions, metrics.ctr FROM campaign WHERE segments.date DURING LAST_30_DAYS ORDER BY metrics.cost_micros DESC LIMIT 25"
    r = requests.post(
        f'https://googleads.googleapis.com/v18/customers/{CUSTOMER_ID}/googleAds:search',
        headers={'Authorization':f'Bearer {token}','developer-token':DEV_TOKEN,'Content-Type':'application/json'},
        json={'query':query}
    )
    return (r.text, r.status_code, {**CORS,'Content-Type':'application/json'})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=10000)
