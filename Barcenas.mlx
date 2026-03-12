% ============================================================
%  DISEÑO DE TANQUE DE ALMACENAMIENTO
%  Análisis hidráulico por trayectoria de chorro libre
% ============================================================

% --- Parámetros de entrada ---
g             = 9.8;          % [m/s²]  Gravedad
hChorro       = 3;            % [m]     Altura máxima del chorro
lengthChorro  = 4;            % [m]     Alcance horizontal del chorro
Cd            = 0.60;         % [-]     Coeficiente de descarga

% Orificio de salida (niple ½" galvanizado – Foset)
% Ref: https://www.mercadolibre.com.mx/...MLM2777464412
MedidaNominal    = 1/2;                          % [in]  Diámetro nominal
radiusNominalCm  = (MedidaNominal * 0.0254) / 2; % [m]   Radio real
areaForFlow      = pi * radiusNominalCm^2;        % [m²]  Área del orificio

% Tiempo de operación
timeInUse = 12 * 60 * 60;    % [s]  12 horas

% ============================================================
%  ANÁLISIS DE TRAYECTORIA (chorro parabólico)
% ============================================================

viY        = sqrt(2 * g * hChorro);    % [m/s]  Velocidad vertical inicial
tiempoAire = (viY / g) * 2;           % [s]    Tiempo total en el aire
viX        = lengthChorro / tiempoAire;% [m/s]  Velocidad horizontal inicial

viFinal = sqrt(viY^2 + viX^2);        % [m/s]  Velocidad resultante de salida
theta   = atand(viY / viX);           % [°]    Ángulo de salida respecto a horizontal

% Cabeza cinética equivalente (altura piezométrica)
realH = viFinal^2 / (2 * g);          % [m]

% ============================================================
%  CÁLCULO DE GASTO Y VOLUMEN
% ============================================================

FlujoV       = Cd * areaForFlow * viFinal;  % [m³/s]  Gasto volumétrico
volumeToUse  = timeInUse * FlujoV;          % [m³]    Volumen útil (12 h)

% ============================================================
%  GEOMETRÍA DEL TANQUE  (planta 4 × 4 m)
% ============================================================

finalFormX = 4;                              % [m]
finalFormY = 4;                              % [m]
finalFormZ = realH + volumeToUse / 4^2;      % [m]  Altura total del tanque

% ============================================================
%  RESULTADOS
% ============================================================

fprintf('\n========================================\n')
fprintf('  RESULTADOS – DISEÑO DE TANQUE\n')
fprintf('========================================\n\n')

fprintf('--- Condiciones del chorro ---\n')
fprintf('  Altura máxima           : %.2f m\n',   hChorro)
fprintf('  Alcance horizontal      : %.2f m\n',   lengthChorro)
fprintf('  Ángulo de salida        : %.2f °\n',   theta)
fprintf('  Velocidad de salida     : %.4f m/s\n', viFinal)

fprintf('\n--- Orificio de salida ---\n')
fprintf('  Diámetro nominal        : %.4f in  (%.6f m)\n', ...
        MedidaNominal, MedidaNominal * 0.0254)
fprintf('  Área del orificio       : %.6e m²\n', areaForFlow)
fprintf('  Coeficiente de descarga : %.2f\n',    Cd)

fprintf('\n--- Hidráulica del tanque ---\n')
fprintf('  Desnivel requerido (H)  : %.4f m\n',  realH)
fprintf('  Gasto constante (Q)     : %.6e m³/s\n', FlujoV)

fprintf('\n--- Almacenamiento (12 h de uso) ---\n')
fprintf('  Tiempo de uso           : 12 horas\n')
fprintf('  Volumen útil            : %.4f m³\n', volumeToUse)

fprintf('\n--- Dimensiones del tanque ---\n')
fprintf('  X = %.1f m\n', finalFormX)
fprintf('  Y = %.1f m\n', finalFormY)
fprintf('  Z = %.4f m  (H_cinética + columna útil)\n', finalFormZ)
fprintf('========================================\n\n')
