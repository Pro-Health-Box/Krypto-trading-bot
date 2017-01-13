![status](https://david-dm.org/ctubio/tribeca.svg)

`tribeca.js` is a very low latency cryptocurrency [market making](https://github.com/ctubio/tribeca/blob/master/MANUAL.md#what-is-market-making) trading bot with a full featured [web client](https://github.com/ctubio/tribeca#web-ui), [backtester](https://github.com/ctubio/tribeca/blob/master/MANUAL.md#how-can-i-test-new-trading-strategies), and supports direct connectivity to [several cryptocoin exchanges](https://github.com/ctubio/tribeca/tree/master/etc#configuration-options). On modern hardware, it can react to market data by placing and canceling orders in under a millisecond.

![Web UI Preview](https://raw.githubusercontent.com/ctubio/tribeca/master/dist/img/web_ui_preview.png)

Runs on the latest node.js (v6 or greater). Persistence is acheived using mongodb. Installation via Docker is supported, but manual installation in a dedicated fresh unix-like instance is recommended.

### Compatible Exchanges

1. Coinbase

2. HitBTC

3. OKCoin

4. Bitfinex

### Docker Installation

See [dist/Dockerfile](https://github.com/ctubio/tribeca/tree/master/dist#dockerfile) section if you use winy or mac.

### Manual Installation

1. Ensure your target machine has node v6 or greater (`nodejs -v`) and mongoDB v3 or greater (`mongo --version`).

2. Clone the repository somewhere with `git clone ssh://git@github.com/ctubio/tribeca`.

3. In the toplevel path of the git cloned repository, `npm install`. This will install all local dependencies in `node_modules` folder and also compile TypeScript in `src` folder to CommonJS in `app` folder.

4. Copy `etc/tribeca.json.dist` to `etc/tribeca.json`, and modify the config keys, see [configuration](https://github.com/ctubio/tribeca/tree/master/etc#configuration-options) section. Point the instance towards the running mongoDB instance (usually just `mongodb://localhost:27017/tribeca`).

5. In the toplevel path of the git cloned repository, `npm start`, or `service tribeca start` anywhere if the optional init script `dist/tribeca-init.sh` is installed.

Optional:

1. Install the system daemon script `dist/tribeca-init.sh`, it requires forever (`npm i -g forever`), see [dist](https://github.com/ctubio/tribeca/tree/master/dist) folder.

2. Replace the certificate at `etc/sslcert` folder with your own, see [web ui](https://github.com/ctubio/tribeca#web-ui) section. But, the certificate provided is a fully featured default openssl, that you may just need to authorise in your browser.

3. Set environment variable TRIBECA_CONFIG_FILE to full path of `tribeca.json` if you run the app manually from other locations with `nodejs path/to/tribeca.js` or with forever globally installed `forever start path/to/tribeca.js`. The environment variable is not needed if the working directory is the root folder where `tribeca.js` is located.

### Configuration

See [etc](https://github.com/ctubio/tribeca/tree/master/etc) folder.

### Application Usage

1. Open your web browser to connect to HTTPS port `3000` of the machine running tribeca. If you're running tribeca locally on Mac/Windows on Docker, replace "localhost" with the address returned by `boot2docker ip`.

2. Read up on how to use tribeca and market making in the [manual](https://github.com/ctubio/tribeca/blob/master/MANUAL.md).

3. Set up trading parameters to your liking in the web UI. Click the "BTC/USD" button so it is green to start making markets.

### Web UI

Once `tribeca` is up and running, visit HTTPS port `3000` of the machine on which it is running to view the admin view. There are inputs for quoting parameters, grids to display market orders, market trades, your trades, your order history, your positions, and a big button with the currency pair you are trading. When you're ready, click that button green to begin sending out quotes. The UI uses a healthy mixture of socket.io and angularjs.

If you want to generate your own certificate see [SSL for internal usage](http://www.akadia.com/services/ssh_test_certificate.html).

In case you really want to use plain HTTP, remove the files `server.crt` and `server.key` inside `etc/sslcert` folder.

### REST API

Tribeca also exposes a REST API of all it's data. It's all the same data you would get via the Web UI, just a bit easier to connect up to via other applications. Visit `http://localhost:3000/data/md` for the current market data, for instance.

### Grafana + InfluxDB + CollectD

Tribeca send metrics periodically to [StatsD plugin of CollectD](https://collectd.org/wiki/index.php/Plugin:StatsD) on default port 8125

You can setup a Grafana instance with a InfluxDB datasource to read the metrics from CollectD send by Tribeca.

The metrics send are:

 * Fair Value
 * Amount available in wallet for buy
 * Amount held in open trades for buy
 * Amount available in wallet for sell
 * Amount held in open trades for sell
 * Total amount available in wallet and held in open trades in BTC currency
 * Total amount available in wallet and held in open trades in Fiat currency

### TEST UNITS

Feel free to run `npm test` anytime.

### Unreleased Changelog:

Added nodejs6, typescript2 and angular2.

Added npm install scripts instead of grunt tasks.

### Release 2.0 Changelog:

Added new quoting styles PingPong, Boomerang, AK-47.

Added cleanup of database records, memory usage and log recording.

Added audio notices, realtime wallet display, and grafana integration.

Added https, dark theme and new UI elements.

Added a bit of love to Kira.

### Release 1.0 Changelog:

see the upstream project [michaelgrosner/tribeca](https://github.com/michaelgrosner/tribeca).

### Donations

nope. but you can donate to your favorite developer today! (or tomorrow!)

or see the upstream project [michaelgrosner/tribeca](https://github.com/michaelgrosner/tribeca).
