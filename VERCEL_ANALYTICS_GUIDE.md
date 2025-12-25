# Vercel Web Analytics Setup Guide

This guide documents how Vercel Web Analytics has been integrated into this blog project.

## Overview

Vercel Web Analytics has been successfully integrated into all pages of this tech blog. The integration uses the plain HTML approach, which is suitable for static HTML sites.

## Implementation Details

### What Was Added

Vercel Web Analytics tracking script has been added to the following files:

- `index.html` - Home page
- `about.html` - About page  
- `contact.html` - Contact page

### Integration Method

For this plain HTML blog, the analytics are implemented using the standard HTML integration approach. Each HTML file now includes:

```html
<!-- Vercel Web Analytics -->
<script>
  window.va = window.va || function () { (window.vaq = window.vaq || []).push(arguments); };
</script>
<script defer src="/_vercel/insights/script.js"></script>
```

This script is placed just before the closing `</body>` tag to ensure minimal impact on page load performance.

## How It Works

1. **View Initialization**: The `window.va` function is initialized to queue any analytics calls that happen before the main tracking script loads.

2. **Script Loading**: The `/_vercel/insights/script.js` script is loaded asynchronously with the `defer` attribute, ensuring it doesn't block page rendering.

3. **Automatic Tracking**: Once loaded, Vercel automatically tracks:
   - Page views
   - Navigation between pages
   - Core Web Vitals
   - User interactions

## Deployment Requirements

### Prerequisites

- A Vercel account (free or paid)
- This project deployed to Vercel
- Vercel CLI installed (optional, for local testing)

### Enabling Web Analytics on Vercel

1. Go to the [Vercel Dashboard](https://vercel.com/dashboard)
2. Select your project
3. Click the **Analytics** tab
4. Click **Enable** to activate Web Analytics
5. Deploy your changes to Vercel

> **Note:** Enabling Web Analytics will add new routes (`/_vercel/insights/*`) after your next deployment.

### Deploy Your App

Use the Vercel CLI to deploy:

```bash
vercel deploy
```

Or, if you've connected your Git repository to Vercel, simply push to your main branch and Vercel will auto-deploy.

## Verifying the Integration

Once deployed to Vercel, you can verify that analytics are working:

1. Visit any page of your blog
2. Open your browser's Developer Tools (F12)
3. Go to the Network tab
4. Look for requests to `/_vercel/insights/view` 
5. These requests confirm that tracking is active

## Viewing Your Analytics

After deployment, you can view your analytics data in the Vercel Dashboard:

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Select your project
3. Click the **Analytics** tab
4. You'll see:
   - Page views and visitors
   - Most visited pages
   - Traffic sources
   - Real-time activity

> **Note:** It may take a few minutes for initial data to appear after first deployment. After a few days of visitor traffic, you'll have comprehensive analytics to explore.

## Important Notes

- **No Installation Required**: Since this is a plain HTML site, there's no need to install the `@vercel/analytics` package. The tracking is handled entirely by the script tag.

- **No Route Support**: The plain HTML implementation does not provide automatic route detection. Each page view is tracked independently.

- **Privacy**: Vercel Web Analytics respects user privacy and complies with GDPR, CCPA, and other privacy regulations. See [Vercel's Privacy Policy](https://vercel.com/legal/privacy-policy) for more details.

## Advanced Features

### Custom Events (Pro/Enterprise Plans)

Users on Vercel Pro and Enterprise plans can track custom events such as:
- Button clicks
- Form submissions
- Video plays
- Product purchases

To track a custom event, use:

```javascript
window.va('event', { name: 'custom_event_name', value: 'event_value' });
```

Example:
```javascript
document.getElementById('subscribe-btn').addEventListener('click', function() {
  window.va('event', { name: 'newsletter_signup', value: 1 });
});
```

### Data Filtering

The Analytics dashboard allows you to filter data by:
- Time range (last 24 hours, 7 days, 30 days, custom)
- Device type (desktop, mobile, tablet)
- Browser
- Country
- Page path

## Next Steps

1. **Enable Analytics**: If not already done, enable Web Analytics in your Vercel project settings
2. **Deploy**: Push your changes to deploy the updated blog with analytics
3. **Monitor**: Check your analytics dashboard to see visitor trends
4. **Optimize**: Use the data to understand what content resonates with your audience

## Troubleshooting

### Analytics not tracking

1. Verify the project is deployed to Vercel (not localhost)
2. Check that Web Analytics is enabled in Vercel project settings
3. Ensure the analytics script loads (check Network tab in DevTools)
4. Wait a few minutes for data to propagate to the dashboard

### Script errors

- The `/_vercel/insights/script.js` route must be available - this is only possible when deployed to Vercel
- Ensure you're not blocking external scripts with browser extensions or CSP rules

## Resources

- [Vercel Web Analytics Documentation](https://vercel.com/docs/analytics)
- [Vercel Analytics Package Documentation](https://vercel.com/docs/analytics/package)
- [Custom Events Setup](https://vercel.com/docs/analytics/custom-events)
- [Privacy and Compliance](https://vercel.com/docs/analytics/privacy-policy)
- [Analytics Pricing](https://vercel.com/docs/analytics/limits-and-pricing)

## Support

For more information about Vercel Web Analytics or if you encounter issues:

- Visit [Vercel Documentation](https://vercel.com/docs)
- Check [Vercel Community](https://vercel.com/community)
- Contact [Vercel Support](https://vercel.com/support)
