BigCommerce-Category-Page-Demo-Videos
=====================================

BigCommerce Category Page Demo Videos that are dynamically pulled from /WebDAV/contents/Videos/ and become trigger-able with a button






================================================================================================
================================================================================================
================================================================================================







#3.  Category Demo Videos
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

================================================================================================

================================================================================================









CategoryPageVideos.html

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


