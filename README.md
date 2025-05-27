# piecewise_linear
% Parameters
Vs = 0:0.1:5; % Voltage source sweep (0 to 5V)
R = 100; % Resistor
Von = 0.7; % Diode on-voltage
Rd = 10; % Diode on-resistance

% Initialize arrays for current
Id = zeros(size(Vs));

% Loop through voltage sweep
for i = 1:length(Vs)
    V = Vs(i);
    
    % Case 1: Diode OFF (Id = 0, Vd < Von)
    if V < Von
        Id(i) = 0;
    else
        % Case 2: Diode ON (Vd = Von + Id * Rd)
        % Circuit equation: V = I * R + Von + I * Rd
        Id(i) = (V - Von) / (R + Rd);
    end
end

% Plot I-V characteristics
figure;
plot(Vs, Id * 1000, 'b-', 'LineWidth', 2);
xlabel('Input Voltage V_s (V)');
ylabel('Diode Current I_d (mA)');
title('I-V Characteristics of Diode Circuit (PWL Model)');
grid on;
