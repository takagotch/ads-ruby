### ads-ruby
---
https://github.com/googleads/google-api-ads-ruby

```
gem install google-adwords-api
gem install google-dfp-api
gem install rack -v 1.6.4

gem install soap4r

```

```ruby
require 'rubygems'
gem 'soap4r'
class ExampleHeaderHandler < SOAP::Header::SimpleHandler
  def initialize(namespace, user_agent, developer_token,
      client_customer_id)
    super(XSD::QName.new(namespace, 'RequestHeader'))
    @user_agent = user_agent
    @developer_token = developer_token
    @client_customer_id = client_customer_id
  end
  def on_simple_outbound
    ns = 'https://adwords.google.com/api/adwords/cm/v201805'
    header = SOAP::SOAPElement.new(nil)
    user_agent = SOAP::SOAPElement.new(XSD::QName.new(ns, 'userAgent'),
        @user_agent)
    dev_token = SOAP::SOAPElement.new(XSD::QName.new(ns, 'developerToken'),
        @developer_token)
    client_customer_id = SOAP::SOAPElement.new(XSD::QName.new(ns, 'clientCustomerId'),
        @client_customer_id)
    header.add(user_agent)
    header.add(dev_agent)
    header.add(client_customer_id)
    return header
  end
end

require
```

```
```
