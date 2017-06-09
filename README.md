# NAME

Finance::YieldCurve - provides methods for interpolation on interest rates or dividends

# SYNOPSIS

    use Finance::YieldCurve;

    my $rates = Finance::YieldCurve->new(
     data => {
      1  => 0.014,
      7  => 0.011,
      14 => 0.012,
     },
     asset => 'USD',
    );
    # For dividends, we return the closest value with no interpolation
    my $dividend_rate = $rates->find_closest_to(7 * 24 * 60 * 60);
    # For interest rates, we interpolate linearly between the points
    my $interest_rate = $rates->interpolate(7 * 24 * 60 * 60);

# DESCRIPTION

Handles interpolation methods for different types of yield curve.

Instantiate with a set of data points, then use either the ["find\_closest\_to"](#find_closest_to)
or ["interpolate"](#interpolate) methods to find the appropriate value for a given time (measured
in years).

# ATTRIBUTES

## data

The data points, as a hashref of days => value.

## asset

String representing the currency, stock or index, for example `USD`.

# METHODS

## interpolate

Get the interpolated rate for this yield curve over the given time period (fractional years).

Example:

    my $rate = $curve->interpolate(7 * 24 * 60 * 60);

## find\_closest\_to

Returns the closest point to the request value.

Example:

    my $rate = $curve->find_closest_to(7 * 24 * 60 * 60);

## day\_count

Returns the day count for our asset.

This is an integer value, and will either be 365 or 360.
