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

require 'soap/wsdlDriver'
wsdl = 'https://adwords.google.com/api/adwords/cm/v201802/CampaignService?wsdl'
campaign_service = SOAP::WSDLDriverFactory.new(wsdl).create_rpc_driver

header_handler = ExampleHeaderHandler.new(namespace, auth_token,
    'test_useragent', dev_token, client_customer_id)
campaign_service.headerhandler << header_handler

selector = {
  :ids => [ campaign_id ]
}
response = campaign_service.get(:selector => selector)
campaign = response.rval.entries.first

bids_element = SOAP::SOAPElement.new(
  SOAP::SOAPElement.to_qname('bids', namespace))
keyword_max_cpc = {
  :amount => {
    :microAmount => 10000000
  }
}
keyword_max_cpc_element = SOAP::Element.from_obj(keyword_max_cpc, namespace)
keyword_max_cpc_element.element = 
  SOAP::SOAPElement.to_qname('bid', namespace)
keyword_max_cpc_element.extraattr('CpcBid', namespace)
  SOAP::SOAPElement.to_qname('CpcBid', namespace)
bids_element.add(keyword_max_cpc_element)
operation = {
  :operand => {
    :name => 'Sample Ad Group - %s' % Time.new,
    :status => 'ENABLED',
    :campaignId => campaign_id,
    :biddingStrategyConfiguration => {
      :bids => bids_element
    }
  },
  :operator => 'ADD'
}
response = ad_group_service.mutate(:operations => [operation])
ad_groups = response.rval.value

```

```
```
