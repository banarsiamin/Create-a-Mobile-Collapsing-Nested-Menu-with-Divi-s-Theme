# Create-a-Mobile-Collapsing-Nested-Menu-with-Divi-s-Theme
How to Create a Mobile Collapsing Nested Menu with Divi’s Theme Builder

Insert CSS & JQuery Code in Header or theme option 
I modified the collapsible mobile menu code to work with the menu built with Divi Theme Builder.

Try to paste the code below in WP Admin > Divi > Theme Options > Integrations > Add code to the body

<style type="text/css">
header .et_mobile_menu .menu-item-has-children > a { background-color: transparent; position: relative; }
header .et_mobile_menu .menu-item-has-children > a:after { font-family: 'ETmodules'; text-align: center; speak: none; font-weight: normal; font-variant: normal; text-transform: none; -webkit-font-smoothing: antialiased; position: absolute; }
header .et_mobile_menu .menu-item-has-children > a:after { font-size: 16px; content: '\4c'; top: 13px; right: 10px; }
header .et_mobile_menu .menu-item-has-children.visible > a:after { content: '\4d'; }
header .et_mobile_menu ul.sub-menu { display: none !important; visibility: hidden !important;  transition: all 1.5s ease-in-out;}
header .et_mobile_menu .visible > ul.sub-menu { display: block !important; visibility: visible !important; }
</style>

<script type="text/javascript">
(function($) {
    
    function setup_collapsible_submenus() {
        var $menu = $('header .et_mobile_menu'),
            top_level_link = 'header .et_mobile_menu .menu-item-has-children > a';
            
        $menu.find('a').each(function() {
            $(this).off('click');
            
            if ( $(this).is(top_level_link) ) {
                $(this).attr('href', '#');
            }
            
            if ( ! $(this).siblings('.sub-menu').length ) {
                $(this).on('click', function(event) {
                    $(this).parents('.mobile_nav').trigger('click');
                });
            } else {
                $(this).on('click', function(event) {
                    event.preventDefault();
                    $(this).parent().toggleClass('visible');
                });
            }
        });
    }
    
    $(window).load(function() {
        setTimeout(function() {
            setup_collapsible_submenus();
        }, 700);
    });
})(jQuery);
</script>
