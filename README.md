# Company Shares Outstanding Dashboard

This single-file, responsive HTML application visualizes the highest and lowest common stock shares outstanding for publicly traded companies, based on data fetched from the SEC EDGAR API.

## Features

-   **Responsive Design:** Built with Tailwind CSS, ensuring a clean and adaptable layout across various screen sizes.
-   **Dynamic Data Fetching:** Displays the entity name, maximum, and minimum common stock shares outstanding along with their fiscal years for a given company.
-   **Live Data from SEC:** Fetches financial data directly from the SEC EDGAR API.
-   **Custom CIK Support:** Allows users to view data for any 10-digit CIK (Central Index Key) by modifying the URL.

## How to Use

1.  **Open `index.html`:**
    Simply open the `index.html` file in your web browser. By default, it will display data for **Ameriprise Financial (CIK: 0000820027)**.

2.  **View Data for a Specific Company:**
    You can specify a different company by appending a `CIK` query parameter to the URL. For example, to view data for **Apple Inc. (CIK: 0000320193)**, you would open:

    `index.html?CIK=0000320193`

    Replace `0000320193` with the 10-digit CIK of any company you wish to look up.

## Data Filtering Logic

The application filters the SEC data (`dei/EntityCommonStockSharesOutstanding`) to include only entries where:
-   The `fy` (fiscal year) is greater than 2020.
-   The `val` (value) is a numeric figure.

From these filtered entries, it identifies the highest and lowest `val` and their corresponding `fy`.

## Technical Details

-   **HTML:** Structure and content.
-   **Tailwind CSS:** For styling and responsiveness.
-   **JavaScript:** For fetching data from the SEC API, parsing the response, filtering, calculating min/max values, and dynamically updating the DOM.
-   **SEC EDGAR API:** The primary data source.
-   **AllOrigins Proxy:** Used to circumvent CORS (Cross-Origin Resource Sharing) restrictions when fetching data from the SEC API from a client-side browser environment. This proxy retrieves the SEC data and serves it back to the client.

### Note on User-Agent

The SEC requests a descriptive `User-Agent` for API requests. While an attempt is made to set this header in the client-side JavaScript `fetch` call, modern browsers often restrict setting custom `User-Agent` headers for security reasons. When using a proxy like AllOrigins, the `User-Agent` will be set by the proxy server, not directly by the client's browser script.