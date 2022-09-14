# wordpress-customization


Important Links 

https://developer.wordpress.org/reference/classes/wp_query/
----------------------------------------------------------------------------------
Register a sidebar 
----------------------------------------------------------------------------------
<code> dynamic_sidebar( 'sidebar-1' );</code>
<code>
   register_sidebar(
   array(
   'name'          => esc_html__( 'Footer-2', 'unipe' ),
   'id'            => 'sidebar-3',
   'description'   => esc_html__( 'Add widgets here.', 'unipe' ),
   'before_widget' => '
   <section id="%1$s" class="widget %2$s">',
      'after_widget'  => '
   </section>
   ',
   'before_title'  => '
   <h2 class="widget-title">',
      'after_title'   => '
   </h2>
   ',
   )
   );
</code>
<code>
register_nav_menus(
array(
'menu-1' => esc_html__( 'Primary', 'unipe' ),
'menu-2' => esc_html__( 'Company', 'unipe' ),
'menu-3' => esc_html__( 'Legal', 'unipe' ),
'menu-4' => esc_html__( 'Contact Us', 'unipe' ),		 
)
);
</code>
<code>
wp_nav_menu(
array(
'theme_location' => 'menu-2',
'menu_id'        => 'Company-menu',
)
);
</code>



----------------------------------------------------------------------------------
custom-post-with-Categories.html
----------------------------------------------------------------------------------
<?php 
  $args = array(
      'post_type' => 'videos',
      'tax_query' => array(
        array(
            'taxonomy' => 'category',
            'field' => 'slug',
            'terms' => 'featuredvideos'
        )
    )
  );
  $the_query = new WP_Query($args); ?>
<?php if ($the_query->have_posts()): ?>
<?php while ($the_query->have_posts()):
        $the_query->the_post();
        $the_title     = get_the_title();
        $the_content   = get_the_content();
        $the_link      = get_permalink();
        $thumbnail_url = get_the_post_thumbnail_url();
        $youtube_id    = do_shortcode('[acf field="youtube_video_id"]'); 
?>
<?php echo $the_link; ?>
<?php echo $youtube_id; ?>
<?php echo $the_title; ?>
<?php echo wp_trim_words(get_the_content(), 20, '...'); ?>
<?php endwhile; wp_reset_postdata(); endif; ?>
