<?php
/**
 * Job listing in the loop.
 *
 * This template can be overridden by copying it to yourtheme/job_manager/content-job_listing.php.
 *
 * @see         https://wpjobmanager.com/document/template-overrides/
 * @author      Automattic
 * @package     wp-job-manager
 * @category    Template
 * @since       1.0.0
 * @version     1.34.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

global $post;
?>
<li <?php job_listing_class(); ?> data-longitude="<?php echo esc_attr( $post->geolocation_long ); ?>" data-latitude="<?php echo esc_attr( $post->geolocation_lat ); ?>">
	<a href="<?php the_job_permalink(); ?>">
		<?php the_company_logo(); ?>
		<div class="position">
		    <div class="company">
				<?php the_company_name( '<p>', '</p> ' ); ?>
			</div>
			<h3><?php wpjm_the_job_title(); ?><?php if(newly_posted_job()) { echo '<span class="new_job">'.esc_html__(' NEW ','').'</span>'; } ?></h3>
		</div>
		<div class="location">
			<?php
                            $terms = get_the_terms( $post->ID, 'job_listing_region' );
                            
                            if ( $terms && ! is_wp_error( $terms ) ) : 
                                
                                $joblocs = array();
                                $max_terms = 2;
                                $count = 0;
                                
                                foreach ( $terms as $term ) {
                                    $count++;

                                    if ($count > $max_terms) {
                                        break;
                                    }
                                    $term_link = get_term_link( $term );
                                    $joblocs[] = $term->name;
                                }
                                
                                $print_locs = join( ", ", $joblocs ); 
                                if ( $count < count($terms) ) {
                                    $remaining_count = count($terms) - $count;
                                    $show_more_link = '<span>plus '.$remaining_count.'more. </a>';
                                    $print_cats .= ' ' . $show_more_link;
                                }
                                ?>
                                <span class="dashicons dashicons-location"></span>
                                <?php echo $print_locs;
                                ?>
                            <?php else :?>
                                
                                <span class="dashicons dashicons-location"></span>
                                <?php the_job_location();
                                ?>
                                
                            <?php endif; ?>
		</div>
		<ul class="meta">
			<?php do_action( 'job_listing_meta_start' ); ?>

			<?php if ( get_option( 'job_manager_enable_types' ) ) { ?>
				<?php $types = wpjm_get_the_job_types(); ?>
				<?php if ( ! empty( $types ) ) : foreach ( $types as $type ) : ?>
					<li class="job-type <?php echo esc_attr( sanitize_title( $type->slug ) ); ?>"><?php echo esc_html( $type->name ); ?></li>
				<?php endforeach; endif; ?>
			<?php } ?>

			<li class="date"><?php the_job_publish_date(); ?></li>

			<?php do_action( 'job_listing_meta_end' ); ?>
		</ul>
	</a>
</li>
