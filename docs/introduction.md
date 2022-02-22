# Introduction to Personalization

Website Personalization is the process of creating customized experiences for visitors to a website. Rather than providing a single experience for all visitors, website personalization allows companies to present visitors with unique experiences tailored to their needs and desires.

## What does this SDK offer?

This SDK offers both Geo and Interest targeting. Below we will go into further detail for each type of targeting.

## Geo Targeting Functionality

## Interest Targeting Functionality

Interests are determined by gathering a visitor's behavioral data when interacting with a site that has the [Pantheon WordPress Edge Integrations plugin](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations/) installed and activated.

Once a visitor browses to 3 or more Posts containing a given taxonomy term, that term (or terms) is considered an Interest. When an Interest is defined, a cookie containing the Interest data is created and pushed to the [HeaderData class](https://github.com/pantheon-systems/pantheon-edge-integrations/). 

Interests can be then fetched from the HeaderData class and used to serve personalized content in a variety of ways, including cached pages, or related content blocks.

### Default Behavior and Available Customizations

Out of the box this plugin uses the default taxonomy, `category`, to determine Interests. This taxonomy can be changed, or added to, using the `pantheon.ei.taxonomy` filter.

The number of views it takes for a term to be considered an Interest is set to 3. This number, or threshold, can be modified using the `pantheon.ei.interest_threshold` filter.

The post type that is used to determine Interests is `post` by default, but can be modified using `pantheon.ei.post_types` filter.

### Testing Interest Targeting

Interests can be tested or verified in a couple of different ways.

The `pantheon.ei.parsed_interest_data` filter is available to get and modify Interest data from the HeaderData class. With the filter, engineers can confirm if an Interest is set, and modify the Interest data before it's returned by the `get_interest` function.

Using the `get_interest` function, engineers can return the Interest(s) from the HeaderData class, which can be used with the `WP_Query` class to fetch personalized content for a given visitor.