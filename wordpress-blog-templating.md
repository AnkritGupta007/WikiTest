## Overview 
CMU Blogging Platforms Project, Project ID: 277776, includes the completion of three custom UComm-approved templates for use by various campus stakeholders. The three templates share the same sub-pages for posts, but have unique front pages each with matching search result pages:  
**CMU_Grid**: Grid with no Sidebar  
**CMU_Gold**: Full-Width (960) with no sidebar  
**CMU_Maroon**: A standard Post-Sidebar feed, each with matching search result pages.  


## Resources & Included Plugins:  
The official WordPress documentation: https://codex.wordpress.org/  

The base template structure for our themes (pre-customization): https://underscores.me/  

The plugin to assist with bootstrap navigation: https://github.com/wp-bootstrap/wp-bootstrap-navwalker  

The plugin that populates the breadcrumb on all sub-pages, consistent with CMU web standards: http://themehybrid.com/plugins/breadcrumb-trail  

Bootstrap (enqueued in functions.php): //cdn.cmich.edu/bootstrap/3.3.7/css/bootstrap.min.css , //cdn.cmich.edu/bootstrap/3.3.7/js/bootstrap.min.js and //cdn.cmich.edu/jquery/jquery.min.js 

Fonts (enqueued in functions.php): https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css and //cdn.cmich.edu/css/fonts/fonts.css

## Customization: 
**All Templates**  
* Google Analytics : The ``gtag`` was added to the top of the ``header.php`` file for each template.

* UComm-Approved Custom Header Images : Preserving the identity standards of the blogs while still allowing for customization includes a selection of header images on the Maroon and Gold templates (Grid has a yellow gradient background so as to not conflict with the layout). The images were cropped and given a transparency gradient prior to being added to each template, and then were added in the ``/img/headers/`` folders as both a full-size .png (to preserve gradient transparency) and .jpg thumbnail preview. The ``functions.php`` file includes a registration array for the default header options, as follows: 
``register_default_headers( array(
			'football' => array(
				'url'           => '%s/img/headers/football_1920.png',
				'thumbnail_url' => '%s/img/headers/football_thumb.jpg',				
				'description'   => __( 'Football', 'cmu' )
			),``  
A default image is designated in ``custom-header.php`` and declared as the last lines in ``header.php``. Within the customizer, the default image may be swapped for any other image within the registered image array.  
  
* Bootstrap Navwalker :  In addition to including the ``wp-bootstrap-navwalker.php`` file and declaring it as ``require_once`` in ``functions.php``, the navwalker function is called in ``header.php`` as an array item in the ``wp_nav_menu``.

* Functions.php and Enqueueing Scripts/Styles : For any page, function or variable to be recognized within the WordPress structure, it must be declared within a functions file - the main for each template being ``functions.php`` - however, each template also has a minor version for more specific controls in ``/inc/template-functions.php``. These files define the existence of aspects like theme support and, in our case, default headers. Stylesheets and scripts must be added here - *not in the index page* and are done as either ``wp_enqueue_style();`` or ``wp_enqueue_script();``. All scripts and styles, such as Font Awesome and Bootstrap, were included using this method.


* The Customizer ``/inc/customizer.php`` : This manages the accessible customization options for blog users - in our case, selecting the blog layout, header image if applicable, contact information and social media. Controls were removed, such as ``	$wp_customize->remove_section('background_image');`` and ``	$wp_customize->remove_section('custom_css');`` to keep a uniform template appearance and remove the ability for users to add custom CSS to their pages (essentially overriding aspects of the UComm-approved template).  

* Unregistering Widgets : The Custom HTML widget within the customizer was removed from user access to ensure the templates stay true to branding. To remove widgets, the ``/inc/unreg-widgets.php`` file was added, and but had to be enqueued as a requirement from ``functions.php``.

* Custom Footer : In addition to the standard CMU footer information, the templates allow for a customizable sub-footer with contact information. If desired, the user can fill out the contact fields from within the Customizer (all fields are required in order for the sub-footer to populate). Each variable was declared as null in the  ``$defaults = array`` of ``/template-functions.php`` file, given ``$wp_customize->add_control`` and ``$wp_customize->add_setting`` parameters in ``/inc/customizer.php`` so that the fields would populate for the users, and then called in the ``/footer.php`` file by transferring in the user-entered contact information and converting to the appropriate html format - displaying the subfooter only if the contact name, address, phone number and email has been entered (the '``$contact_name`` has an ``if-else`` statement to create a link if a department/personal website is included, or plain text if not).	

* Social Media : The same process as in the **Custom Footer** controls was used to allow for user input of social media links in the header of their blogs. The social media buttons only appear in the header if a link has been provided in the customizer, and are written into the ``header.php`` file as ``$facebook= cmu_get_option( 'facebook' ); //Facebook link, if applicable``  followed by the column formatting that includes the link list for the social media Font Awesome icons and links.

* Header Image Upload Button Removal : We wanted to give the ability to customize the background/header images for the blogs while ensuring that they remained within the approved branding guidelines. An array of images is provided within the templates, but the selection area within the Customizer also has a media upload button by default. It was discovered that some of the controls within the Customizer are locked down further by the WordPress Core (and not documented publicly for override). To solve this issue, an additional action (``add_action( 'admin_print_styles', 'my_admin_css' );``) and function  
``function my_admin_css(){
	if( is_admin() ) {
	 wp_enqueue_style(
		 "media_upload", 
		 get_bloginfo('template_directory')."/layouts/custom_admin.css", 
		 false, 
		 false, 
		 "all"
	 );
	}
 }`` were added to the ``/functions.php`` file, which call the ``/layouts/custom_admin.css`` file and use CSS to remove/hide the upload button. 

* Search Forms : There are two search forms for the templates to accommodate the standard WordPress sidebar search function, as well as the requested search bar in the header, similar to the cmich.edu websites. Respectively, these forms are  ``searchform.php`` (declared as default in ``functions.php`` and called from ``sidebar.php``) and ``headerSearchform.php``(called from ``header.php``). Having two form controls allowed for individual formatting based on the location of the search form within each template.

**CMU_Grid**  
* ``/index.php`` : The main page has a 3x3 grid layout for post display, which uses two ``($counter % 3 == x)`` to determine bootstrap row breaks.   


  


* Title maximum length : Parameters were included on ``index.php`` and ``search.php`` to limit the post title length so that it doesn't overflow the grid format. When the posts are called from these pages, they include ``add_filter('the_title', 'max_title_length');`` before the navigation array and ``remove_filter( 'the_title', 'max_title_length');`` after to ensure that the title doesn't overflow the navigation row with the navigational chevrons. These functions were declared in the ``template-functions.php`` file, as ``function max_title_length( $title )`` and ``function max_navtitle_length( $title )``.



## File Structure:  

[CMU_Grid.pdf](/uploads/857a42100002e98fac58a4eafb562457/CMU_Grid.pdf)

## Tags
[[WordPress]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WordPressTag)