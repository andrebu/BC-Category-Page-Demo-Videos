BigCommerce-Category-Page-Demo-Videos
=====================================

BigCommerce Category Page Demo Videos that are dynamically pulled from /WebDAV/contents/Videos/ and become trigger-able with a button


================================================================================================

###TODO

1. ~~Fix behavior - when out of stock and with video, neither appears.~~
2. Not showing up on brands.
3. When with video, shows “HasVideo” on receipt/invoice.
4. Integrate the "videoDemo" div into JS and out of BC panel

================================================================================================

## Installation

3.1 - Add /* Category Product List Video */ CSS
3.2 - Add CategoryPageVideos.html Panel to Panels/CategoryContent.html
                            %%GLOBAL_CategoryProductListing%%
                            %%Panel.CategoryPageVideos%%                            
                        </ul>
                        
3.3 - Add JavaScript--that hides the "Options HasVideo" trigger--to Snippets/ProductAddToCart.html
3.4 - Add 'div.categoryDemoVideo' HTML to Snippets/CategoryProductsItem.html 
    <div class="ProductImage QuickView" data-product="%%GLOBAL_ProductId%%">
        %%GLOBAL_ProductThumb%%
        <div class="categoryDemoVideo" class="%%GLOBAL_ProductId%%"></div>
    </div>

3.5 - Create Videos folder in WebDav (/dav/Content/Videos) and add .mp4/.ogv/.webm videos with the ProductID.  Example:  
	<li class="Odd " style="min-height: 472px; position: absolute; left: 0px; top: 0px;">
		<div class="ProductImage QuickView" data-product="296"> <!--  --> 
		<!-- The ProductID is the number value of 'data-product="###"' -->
		
3.6 - Remind to add "HasDemoVideo" Option (checkbox, value field) to Product Option Set

3.4 - Video over product listing Popup
						...
                        <ul class="ProductList %%GLOBAL_DisplayMode%%">
                            %%GLOBAL_CategoryProductListing%%
                            
<script type="text/javascript">

$(".Options").each(function checkForVideo(url) {

	var ProductCatOpt = $(this);
		ProductId = $(this).parent().parent().find('div.ProductImage').attr('data-product');

	function ajax1() {
	    return $.ajax('/content/videos/'+ProductId+'.mp4')
		    .done(function() { 
		        $(ProductCatOpt).addClass('withVideo');
		    }).fail(function() { 
		    	return;
		    });
		}
		$.when(ajax1()).done(function(a1){

	        $('.withVideo').closest('li').append('<span class="videoDemoBtn"><div class="triangle"></div></span>');
	
	        $('.videoDemoBtn').click(function() {    
	
	        if($(this).hasClass('videoPlaying')) {
	            $(this).removeClass('videoPlaying');
	            $(this).parent().find('img').show();
	            $(this).parent().find('div.categoryDemoVideo').hide().html('');
	            }
	            else {
	        
	                var ProductId = $(this).parent().find('div.ProductImage').attr('data-product');
	                $(this).addClass('videoPlaying');
	                $(this).parent().find('img').hide();        
	                $(this).parent().find('div.categoryDemoVideo').show().html('<video id="demoVideo" class="video" preload="auto" autoplay="autoplay" loop="loop" autobuffer="autobuffer" muted="muted" controls="controls" width="100%" height="100%"><source src="https://store-mixi7d.mybigcommerce.com/content/videos/'+ProductId+'.mp4"><source src="https://store-mixi7d.mybigcommerce.com/content/videos/'+ProductId+'.ogv" type="video/ogg"><p>Your browser does not support this video.  Please upgrade your browser!</p></video>');
	                        }
	                });

            });


/*
	var video = document.getElementById('demoVideo');
	video.addEventListener('click',function(){
	  video.play();
	},false);
*/


        });

</script>
                            
                        </ul>
                        ...

3.5 - Add following JS to Snippets/ProductAddToCart.html
...
<!-- //Custom Add to Wishlist -->
//]]></script>

%%GLOBAL_EventDateJavascript%%

<script language="javascript" type="text/javascript">
            $('.productAttributeList').find("span:contains('HasDemoVideo')").closest('.productAttributeRow').hide();
</script>






================================================================================================

## Using

To get this to work, you just need to require the module once per run-time, like so.

    Just install and it'l do the work for you!

================================================================================================

## Other BigCommerce modules

* [BigCommerce Product Page Demo Videos](https://github.com/iamandrebulatov/BigCommerce-Product-Page-Demo-Videos)
* [BigCommerce Product Page Brand Descriptions](https://github.com/iamandrebulatov/BigCommerce-Product-Page-Brand-Descriptions)
* [BigCommerce Product Page Brand Logos](https://github.com/iamandrebulatov/BigCommerce-Product-Page-Brand-Logos)
* [BigCommerce Category Page Color Swatch](https://github.com/iamandrebulatov/BigCommerce-Color-Swatch-On-Category)
* [BigCommerce Category Page 2nd Alternate Thumbnail](https://github.com/iamandrebulatov/BigCommerce-Category-Pages-2nd-Alternate-Thumbnail)
* [BigCommerce Category Page Videos](https://github.com/iamandrebulatov/BigCommerce-Category-Page-Demo-Videos)
* [BigCommerce Category Page Out of Stock Ribbons](https://github.com/iamandrebulatov/BigCommerce-Out-of-Stock-Category-Items)


## Support

> ⚐ Please help me spend more time developing and maintaining awesome modules like this by donating!

The absolute best thing to do is to sign up with [ChangeTip](//changetip.com) or [GratiPay](//gratipay.com) if you haven't already and donate just $1 a week. That is roughly a cup of coffee per month. Also, please do donate to many other amazing open source projects!

[![ChangeTip donate button](http://andrebulatov.com/wp-content/uploads/tipme_button.png)](//www.changetip.com/tipme/andre.bulatov/ "Donate once-off to this project using ChangeTip")
[![GratiPay donate button](http://andrebulatov.com/wp-content/uploads/gratipay-button.png)](//www.gratipay.com/andrebulatov/ "Donate once-off to this project using GratiPay")


## License

The MIT License (MIT)

Copyright (c) 2014 Andre Bulatov

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
