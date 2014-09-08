---
layout: post
title: "Simple Awesome"
date: 2014-09-06 15:26:07 +1000
comments: true
categories: 
---

## Something you ought to know
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tu enim ista lenius, hic Stoicorum more nos vexat. Duo Reges: constructio interrete. Habes, inquam, Cato, formam eorum, de quibus loquor, philosophorum. Quos nisi redarguimus, omnis virtus, omne decus, omnis vera laus deserenda est. Hic quoque suus est de summoque bono dissentiens dici vere Peripateticus non potest. Sic consequentibus vestris sublatis prima tolluntur.

{% codeblock lang:ruby %}
class Location < ActiveRecord::Base
  GOOGLE_API_KEY = "AIzaSyBYfAWEkh07uIztHgGzUmfJAFNnpCV7sZw"

  extend FriendlyId
  friendly_id :city, use: [:slugged, :scoped], :scope => :country_code

  searchkick text_start: [:country, :city]

  has_many :events
  has_many :profiles
end

{% endcodeblock %}
