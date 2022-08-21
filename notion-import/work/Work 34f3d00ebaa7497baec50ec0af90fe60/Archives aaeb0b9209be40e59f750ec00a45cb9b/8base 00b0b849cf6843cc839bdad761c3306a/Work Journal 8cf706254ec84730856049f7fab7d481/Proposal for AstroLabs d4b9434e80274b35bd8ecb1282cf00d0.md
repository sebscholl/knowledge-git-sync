# Proposal for AstroLabs

Created: January 7, 2020 5:21 PM

Project price $100,000 engagement (say it's a 33% discount since design is taken out of the equation).

The scope of this project contains the deliverables required for a successful beta launch. That includes:

- User roles:
    1. CollectorRole - A normal AstroLabs app user.
        1. Can manage their own profile and settings.
        2. Can manage their own collections wish lists.
        3. Can create and manage their own trades.
    2. ValidatorRole - A validator that's authorized by the AstroLabs partner network.
        1. Can update trades that they've been assigned to validate.
        2. Can update workflow statuses associated with trades.
    3. AdminRole - An AstroLabs employee with an 8base login.
        1. Can manage user profiles and settings.
        2. Can manage all trades.
        3. Can update workflow statuses associated with trades.
        4. Can manage AstroLabs item catalogs.
        5. Can manage user's collections wish lists.
        6. Can block user's with counterfeit inventory. 

- PWA customer application (web + mobile responsive)  with the listed flows enabled:
    1. User login / sign-up / logout flows.
    2. User on-boarding flow: 
        1. A new user should be guided through the steps of building out their profile and adding their existing sneaker collection.
    3. Browsing and searching flow: 
        1. A user should be able to explore or search for sneakers on AstroLabs, whether or not AstroLabs currently has inventory for that make and model through the network.
        2. Every sneaker needs it's own details page, through which existing inventory is aggregated and trades can be initiated.
    4. List management flows:
        1. A user should be able to create multiple wish lists (i.e. *Dream Jordans* and *Retro Kicks*) and manage those lists with ease.
        2. A user should be able to configure different settings for a wishlist (i.e. the list is public or private, should trades be automatically recommended using this list)
    5. Collection management flows:
        1. A user should be able to add to and manage their collection.
        2. A user should be able to select items from AstroLabs existing catalogue when adding to their collection, and then only be asked to specify item specific attributes (i.e. size, color, condition)
        3. A user should be asked to upload photos of the item if it is in used condition, while be able to use stock photos for items in *new* condition.
        4. A user should be able to configure settings for  items in their own collection (i.e. private or public)
    6. User profile flows:
        1. A user should be able to add and update default information to their AstroLabs profile, including things like:
            1. Profile picture
            2. username
            3. bio
            4. social profile links
            5. default shipping address
            6. payment information (connected payment account - e.i. PayPal)
        2. A user should be able to add and update item preferences (i.e. favorite brands, preferred sizes)
    7. Trade management flows:
        1. A user should be able to initiate a trade by specifying one or more items from their own inventory in exchange for one or more items from another users inventory, optionally with a cash amount to be exchanged from one party to the other. 
        2. A user should be able to rescind any trade offer they've made before it is accepted or countered by the recipient.
        3. A user should be able to review a list and the details of all the trade offers they've made, received, completed, rejected, and are currently engaged in.
        4. A user should be able to counter a trade by updating the specified terms (i.e. select different items from either parties inventory and/or change the cash amount to be exchanged).
        5. A user should be able to reject a trade.
        6. A validator should be able to review all the trades that they've historically verified or rejected.
    8. Shipping and Status flows (after a trade has been accepted):
        1. A user should automatically receive a shipping label for where to send their inventory (email or in-app). 
        2. A user should be walked through the steps required to ship their items to the appropriate *verifier*, as well as specify an address the the *verifier* will ship the items they'll be receiving to.
        3. A user and validator should be able to check the status of any trade, and see whether:
            1. Items are waiting to be shipped
            2. Items have shipped
            3. Items have been received by the verifier
            4. Items validated by verifier
            5. Items have been rejected by verifier.
            6. Items have been accepted by verifier and are awaiting shipment (returned to owner or recipient)
            7. (OPTIONAL) If cash needs to be sent:
                1. Awaiting P2P cash transfer.
                2. Cash sender indicates that transfer has been made.
                3. Cash receiver indicates that transfer has been recieved.
            8. Items have shipped from verifier (returned to owner or recipient)
            9. Both parties have received their items (returned to owner or recipient)
            10. Trade completed
        4. A validator should be able to see the trades being shipped to them, as well as update when items have been received, verified/rejected, and reshipped.
    9. Notifications and Pending Task flows:
        1. A user should be notified of **whenever an update is made that demands a subsequent action**, as well as status notifications ****(i.e. "Trade accepted! It's time to ship your items" and "The verifier has shipped your items!")**.**
        2. A notification that's associated with a pending task item should direct the user to the associated view/screen. 
        3. A user should be led through the on-boarding steps of filling out their profile and uploading their 1st item to a *Collection* (i.e. conceptually a *Collection* should be generic, though initially it will be sneakers)
    10. Dispute flows:
        1. A user should be able to contact AstroLabs with disputes and concerns related to trades.

- 3rd Party Integrations
    1. Payment flow (options include PayPal API, Braintree API, [Authorize.net](http://authorize.net) API, manual confirmation):
        1. A user should be able to link up a payment provider or enter credit card information so that AstroLabs can charge both parties once a trade is ... (initialized, verified, or completed).
        2. A user should be able to send a cash payment to another user and indicate (manually or automatically, depending on the provider) once that payment has been made.
        3. A user should be able to indicate (manually or automatically, depending on the provider) whether they have received a payment promised to them in a trade.
    2. Shipping flow (options include Shippo, EasyPost, ShipStation, manual input):
        1. A user should receive a shipping label on trade confirmation or input a tracking number after a trade has been approved.
        2. All parties involved in a trade should receive updates on a shipment **as they are updated by the shipper**. 
        3. A validator should receive shipping labels for all items, along with manifests for each box, after they have rejected or verified the items.

- Administration views
    1. 8base admin dashboard:
        1. An administrator should be able to log into 8base to manage trades.
        2. An administrator should maintain full access to the 8base backend to manage records.
    
    *(Note: The scope of this initial engagement does not include the administrative workflows apps)*