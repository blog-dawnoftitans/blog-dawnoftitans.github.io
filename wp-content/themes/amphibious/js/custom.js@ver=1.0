/*!
 * Custom v1.0
 * Contains handlers for the different site functions
 *
 * Copyright (c) 2019 TemplatePocket.com
 * License: GNU General Public License v2 or later
 * http://www.gnu.org/licenses/gpl-2.0.html
 */

/* global enquire:true */

( function( $ ) {
	var amphibious = {

		// Responsive Menu Build
		responsiveMenuBuild: function () {
			// Site Header Menu Wrapper
			var $menuWrapper = $( '.site-header-menu-wrapper' );

			// Add dropdown toggle that display child menu items.
			$( '.site-header-menu .page_item_has_children > a, .site-header-menu .menu-item-has-children > a' ).append( '<button class="dropdown-toggle" aria-expanded="false"/>' );
			$( '.site-header-menu .dropdown-toggle' ).off( 'click' ).on( 'click', function( e ) {
				e.preventDefault();
				$( this ).toggleClass( 'toggle-on' );
				$( this ).parent().next( '.children, .sub-menu' ).toggleClass( 'toggle-on' );
				$( this ).attr( 'aria-expanded', $( this ).attr( 'aria-expanded' ) === 'false' ? 'true' : 'false' );
			} );

			// Add Close Button Markup
			$menuWrapper.prepend( '<div class="site-header-menu-responsive-close-wrapper"><button class="site-header-menu-responsive-close">&times;</button></div>' );
		},

		// Responsive Menu Destroy
		responsiveMenuDestroy: function () {
			// Site Header Menu
			var $menuWrapper = $( '.site-header-menu-wrapper' );

			// Remove Dropdown Toggles
			$menuWrapper.find( '.dropdown-toggle' ).remove();

			// Remove Close Button
			$menuWrapper.find( '.site-header-menu-responsive-close-wrapper' ).remove();
		},

		// SF Menu Build
		sfMenuBuild: function () {
			// Superfish Menu
			$( 'ul.sf-menu' ).superfish( {
				delay: 1500,
				animation: { opacity: 'show', height: 'show' },
				speed: 'fast',
				autoArrows: false,
				cssArrows: true,
			} );
		},

		// SF Menu Destroy
		sfMenuDestroy: function () {
			// Superfish Menu Destroy
			$( 'ul.sf-menu' ).superfish( 'destroy' );
		},

		// Big Screen Match
		bigScreenMatch: function () {
			// Site Header Menu Wrapper
			var $menuWrapper = $( '.site-header-menu-wrapper' );
			$menuWrapper.removeClass( 'site-header-menu-responsive-wrapper' );

			// Site Header Menu
			var $menu = $( '.site-header-menu' );
			$menu.removeClass( 'site-header-menu-responsive' );
			$menu.addClass( 'sf-menu' );

			// Superfish Menu Build
			amphibious.sfMenuBuild();
		},

		// Big Screen UnMatch
		bigScreenUnMatch: function () {
			// Superfish Menu Destroy
			amphibious.sfMenuDestroy();

			// Site Header Menu
			var $menu = $( '.site-header-menu' );
			$menu.addClass( 'site-header-menu-responsive' );
			$menu.removeClass( 'sf-menu' );

			// Site Header Menu Wrapper
			var $menuWrapper = $( '.site-header-menu-wrapper' );
			$menuWrapper.addClass( 'site-header-menu-responsive-wrapper' );
		},

		// Small Screen Match
		smallScreenMatch: function () {
			// Responsive Menu Build
			amphibious.responsiveMenuBuild();

			// Sliding Panels for Menu
			amphibious.slidePanelInit();

			// Responsive Tables
			$( '.entry-content, .sidebar' ).find( 'table' ).wrap( '<div class="table-responsive"></div>' );
		},

		// Small Screen UnMatch
		smallScreenUnMatch: function () {
			// Responsive Menu Destroy
			amphibious.responsiveMenuDestroy();

			// Responsive Menu Close
			amphibious.slidePanelCloseInit();

			// Responsive Tables Undo
			$( '.entry-content, .sidebar' ).find( 'table' ).unwrap( '<div class="table-responsive"></div>' );
		},

		// Open Slide Panel - Responsive Mobile Menu
		slidePanelInit: function () {
			// Elements
			var $menuWrapper = $( '.site-header-menu-wrapper' );
			var $overlayEffect = $( '.overlay-effect' );
			var $menuClose = $( '.site-header-menu-responsive-close' );

			// Responsive Menu Slide
			$( '.toggle-menu-control' ).off( 'click' ).on( 'click', function( e ) {
				// Prevent Default
				e.preventDefault();
				e.stopPropagation();

				// ToggleClass
				$menuWrapper.toggleClass( 'show' );
				$overlayEffect.toggleClass( 'open' );

				// Slide Panel Open Logic
				if ( $overlayEffect.hasClass( 'open' ) ) {
					// Add Body Class
					$( 'body' ).addClass( 'has-responsive-menu' );

					// Responsive Menu Focus
					amphibious.responsiveMenuFocus();

					// Bring focus to first element
					setTimeout( function() {
						$( '.site-header-menu-responsive-close' ).focus();
					}, 300 );
				}
			} );

			// Responsive Menu Close
			$menuClose.off( 'click' ).on( 'click', function( e ) {
				// Prevent Default
				e.preventDefault();
				e.stopPropagation();

				// Close Slide Panel
				amphibious.slidePanelCloseInit();
			} );

			// Overlay Slide Close
			$overlayEffect.off( 'click' ).on( 'click', function() {
				amphibious.slidePanelCloseInit();
			} );
		},

		// Close Slide Panel
		slidePanelCloseInit: function () {
			// Elements
			var $menuWrapper = $( '.site-header-menu-wrapper' );
			var $overlayEffect = $( '.overlay-effect' );

			// Slide Panel Close Logic
			if ( $overlayEffect.hasClass( 'open' ) ) {
				// Remove Body Class
				$( 'body' ).removeClass( 'has-responsive-menu' );

				// For Menu
				if ( $menuWrapper.hasClass( 'show' ) ) {
					$menuWrapper.toggleClass( 'show' );
				}

				// Toggle Overlay Slide
				$overlayEffect.toggleClass( 'open' );

				// Bring focus to menu control
				setTimeout( function() {
					$( '.toggle-menu-control' ).focus();
				}, 300 );
			}
		},

		// Responsive Menu Focus
		responsiveMenuFocus: function () {
			// Key Down
			$( document ).on( 'keydown', function( e ) {
				// Wrapper Selector
				var selectorWrapper = '.site-header-menu-wrapper';

				// Close Button
				var selectorCloseButton = selectorWrapper + ' > div > button';

				// Parent Anchors
				var selectorParentAnchors = selectorWrapper + ' > ul > li > a';
				// Parent Toggles
				var selectorParentToggles = selectorWrapper + ' > ul > li > a > button';

				// Child Anchors
				var selectorChildAnchors = selectorWrapper + ' > ul > li ul.sub-menu.toggle-on > li > a';
				// Child Toggles
				var selectorChildToggles = selectorWrapper + ' > ul > li ul.sub-menu.toggle-on > li > a > button';

				// Build Selector
				var selector = selectorCloseButton + ',' + selectorParentAnchors + ',' + selectorParentToggles + ',' + selectorChildAnchors + ',' + selectorChildToggles;

				// Elements Query
				var $elements = $( selector );
				var elementsArray = Array.prototype.slice.call( $elements );

				// Elements
				var $lastElement = elementsArray[ elementsArray.length - 1 ];
				var $firstElement = elementsArray[0];
				var $focusedElement = $(':focus')[0];

				// Keys
				tabKey = e.keyCode === 9;
				shiftKey = e.shiftKey;

				// Last Element Matched
				if ( ! shiftKey && tabKey && $lastElement == $focusedElement ) {
					e.preventDefault();
					$firstElement.focus();
				}

				// First Element Matched
				if ( shiftKey && tabKey && $firstElement == $focusedElement ) {
					e.preventDefault();
					$lastElement.focus();
				}
			});
		},

		// Responsive Videos
		responsiveVideosInit: function () {
			$( '.entry-content, .sidebar' ).fitVids();
		},

		// Widget Logic
		widgetLogicInit: function () {
			// Social Menu Widget
			$( '.widget_nav_menu > div[class^="menu-social-"] > ul > li > a' ).wrapInner( '<span class="screen-reader-text"></span>' );

			// Custom Menu Widget
			$( '.widget_nav_menu .menu-item-has-children > a' ).append( '<span class="custom-menu-toggle" aria-expanded="false"></span>' );
			$( '.widget_nav_menu .custom-menu-toggle' ).off( 'click' ).on( 'click', function( e ) {
				e.preventDefault();
				$( this ).toggleClass( 'toggle-on' );
				$( this ).parent().next( '.sub-menu' ).toggleClass( 'toggle-on' );
				$( this ).attr( 'aria-expanded', $( this ).attr( 'aria-expanded' ) === 'false' ? 'true' : 'false' );
			} );

			// Pages Widget
			$( '.widget_pages .page_item_has_children > a' ).append( '<span class="page-toggle" aria-expanded="false"></span>' );
			$( '.widget_pages .page-toggle' ).off( 'click' ).on( 'click', function( e ) {
				e.preventDefault();
				$( this ).toggleClass( 'toggle-on' );
				$( this ).parent().next( '.children' ).toggleClass( 'toggle-on' );
				$( this ).attr( 'aria-expanded', $( this ).attr( 'aria-expanded' ) === 'false' ? 'true' : 'false' );
			} );

			// Categories Widget
			$( '.widget_categories' ).find( '.children' ).parent().addClass( 'category_item_has_children' );
			$( '.widget_categories .category_item_has_children > a' ).append( '<span class="category-toggle" aria-expanded="false"></span>' );
			$( '.widget_categories .category-toggle' ).off( 'click' ).on( 'click', function( e ) {
				e.preventDefault();
				$( this ).toggleClass( 'toggle-on' );
				$( this ).parent().next( '.children' ).toggleClass( 'toggle-on' );
				$( this ).attr( 'aria-expanded', $( this ).attr( 'aria-expanded' ) === 'false' ? 'true' : 'false' );
			} );
		},

		// Media Queries
		mqInit: function () {
			enquire
				.register( 'screen and ( min-width: 992px )', {
					match() {
						// Big Screen Match
						amphibious.bigScreenMatch();
					},
					unmatch() {
						// Big Screen UnMatch
						amphibious.bigScreenUnMatch();
					},
				} )
				.register( 'screen and ( max-width: 991px )', {
					match() {
						// Small Screen Match
						amphibious.smallScreenMatch();
					},
					unmatch() {
						// Small Screen UnMatch
						amphibious.smallScreenUnMatch();
					},
				} );
		},
	};

	// Document Ready
	$( document ).ready( function() {
		// Responsive Videos
		amphibious.responsiveVideosInit();

		// Widget Logic
		amphibious.widgetLogicInit();

		// Media Queries
		amphibious.mqInit();
	} );

	// Document Keyup
	$( document ).keyup( function( e ) {
		// Escape Key
		if ( e.keyCode === 27 ) {
			// Make the escape key to close the slide panel
			amphibious.slidePanelCloseInit();
		}
	} );
}( jQuery ) );
